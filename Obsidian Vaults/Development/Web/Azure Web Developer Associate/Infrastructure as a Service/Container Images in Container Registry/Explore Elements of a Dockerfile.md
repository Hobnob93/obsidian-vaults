#azure #azure-wda #shell 

# Explore Elements of a Dockerfile
Need to understand elements of Dockerfile if you want to create a custom container.
A Dockerfile is a text file containing instructions used to build and run a Docker image.

The following aspects are defined:
- Base or parent image used to create new image
- Commands to update base OS and install additional software
- Build artefacts to include, such as an application
- Services to expose, such as storage or network config
- Command tor un when container is launched

## Example
An example for creating a Docker image for an ASP.NET Core website.

### 1: Specify Parent Image for New Image
```shell
FROM ubuntu:18.04
```

### 2: Update OS Packages & Install Software
```shell
RUN apt -y update 
	&& apt install -y wget nginx software-properties-common apt-transport-https
	&& wget -q <ubuntu18.04configaddr> -O packages-microsoft-prod.deb
	&& dpkg -i packages-microsoft-pod-deb
	&& add-apt-repository universe
	&& apt -y update
	&& apt install -y dotnet-sdk-3.0
```

### 3: Configure Nginx Environment
```shell
CMD service nginx start
COPY ./default/etc/nginx/sites-available/default
```

### 4: Configure Work Directory
```shell
WORKDIR /app
```

### 5: Copy Website Code to Container
```shell
COPY ./website/. .
```

### 6: Configure Network Requirements
```shell
EXPOSE 80:8080
```

### 7: Define Entry Point of Process Running Container
```shell
ENTRYPOINT ["dotnet", "website.dll"]
```

## Summary
Note there are many commands; any combination of commands allows for manipulation of the structure of the image.

Each of the steps creates a cached container image as we build the final container image.
These temporary images are layered on top of each other and presented as a single instance after all the steps.

The `ENTRYPOINT` step indicates which process will execute once we run a container from an image.