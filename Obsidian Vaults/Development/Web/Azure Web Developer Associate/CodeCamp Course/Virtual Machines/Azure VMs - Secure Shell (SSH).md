#azure #az-204 #cli 

Very common way to authenticate to VMs.
Uses SSH key pairs, which needs to be generated.
- Private key
- Public key
Can sue the following command to generate them.
```Shell
ssh-keygen -t rsa
```

The private key should remain on the local system and not be shared with anyone.
The public key is stored on the VM.
When you try to SSH, provide your private key and it will be matched against the public key to authenticate you.
```Shell
ssh -i ~/.ssh/id_rsa.pub azureuser@10.111.12.123
```

You know it's a public key when it ends in `.pub`.