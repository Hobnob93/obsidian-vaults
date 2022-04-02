#azure #az-204 #security

# Configure Security Certificates
*Azure App Service* has tools that let you create, upload, or import a private or public certificate.

Certificates are stored in a deployment unit that is bound to plan's resource group and region combination (called a ==webspace==).
This makes it accessible to other apps in the same resource group and region combination.

Options for adding certificates in *App Service*:
1. Create a free *App Service* managed certificate
	- Private certificate
	- Free
	- Easy to use if you just want to secure your custom domain
2. Purchase an *App Service* certificate
	- Private certificate
	- Managed by *Azure*
	- Combines simplicity of automated certificate management and flexibility of renewal and export options
3. Import a certificate from [[Azure Key Vault|Key Vault]]
	- Useful if you use *Azure Key Vault* to manage your certificates
4. Upload a private certificate
	- If you already have a private certificate from a third party provider
5. Upload a public certificate
	- Public certificates are **not** used to secure custom domains
	- Can load them into your app if you need them to access remote resources

## Private Certificate Requirements
The ***App Service* managed certificate** and ***App Service* certificate** already satisfy the requirements of *App Service*.

Any other private certificates need to meet the following criteria:
- Exported as password-protected `PFX` file
- Encrypted using `triple DES`
- Contains private key at least 2,048 bits long
- Contains all intermediate certificates in the certificate chain

To secure a custom domain in a `TLS binding`, it has additional requirements:
- Contains an ==Extended Key Usage== for server authentication (`OID = 1.3.6.1.5.5.7.3.1`)
- Signed by a trusted certificate authority

## Creating a Free Managed Certificate
*App Service* must be a `Basic`, `Standard`, `Premium`, or `Isolated` [[Examine Azure App Service Plans#Pricing Tiers|pricing tier]].
Custom SSL is not supported in the `F1` or `D1` tier.

The free managed certificate is a ==turn-key solution== for securing a custom DNS name.
It's a ==TSL/SSL== server certificate fully managed by *App Service*.
It is renewed continuously and automatically in six-month intervals, 45 days before expiration.
You create the certificate and bind it to a custom domain - *App Service* will handle the rest.

The free certificate comes with the following limitations:
- Does not support wildcard certificates
- Does not support usage as a client certificate by a certificate thumbprint
- Is not exportable
- Not supported on *App Service Environment* (ASE)
- Not supported with root domains that are integrated with *Traffic Manager*
- If a certificate is for a ==CNAME-mapped domain==, the CNAME must be mapped directly to `<app-name>.azurewebsites.net`

## Import an App Service Certificate
If you purchase a certificate, *Azure* manages the following tasks:
- Takes care of purchase process from *GoDaddy*
- Performs domain verification of the certificate
- Maintains certificate in [[Azure Key Vault]]
- Manages certificate renewal
- Synchronises certificate automatically with imported copies in *App Service apps*

If you already have a working *App Service* certificate, you can:
- Import certificate into *App Service*
- Manage certificate, such as renew, rekey, and export it

## Upload a Private Certificate
If there are multiple certificates in a chain, you need to **merge** them together, before exporting with private key the certificate was generated with.

If you generated your certificate with ==OpenSSL==, then you have created a ==private key file==.
To export to `PFX`, you can run the command below.
```shell
openssl pkcs12 -export -out myserver.pfx -inkey <private-key-file-path> -in 
    <merged-certificate-file-path>
```
When prompted, define an export password - to be used when uploading to *App Service*.

## Enforce HTTPS
By default, anyone can still access app using `HTTP`.
You can redirect all `HTTP` requests to `HTTPS` port.
Can do this through ==TLS/SSL Settings== within *Azure Portal* and enabling `HTTPS Only`.