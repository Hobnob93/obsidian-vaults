#azure #az-204 

Digital Certificates can end with a variety of extensions, such as `.crt`, `.pem`, `.cer`, `.der`, `.p12`, `.pfx`.

#### Privacy Enhanced Mail (PEM)
Base-64 ASCII, so easily human readable.
Most common format for x.509 certificates, CSRs, and cryptographic keys.
PEMs normally have the following extensions:
- `.crt`, `.pem`, `.cer`, and `.key` (for private keys)

#### Distinguished Encoding Rules (DER)
Binary encoding, making it hard for a human to read and edit.
Used for both x.509 certificates and private keys.
DER normally have the following extensions:
- `.der`, `.cer`.

#### Certificate File (CER/CRT)
Base-64 ASCII, so easily human readable.
CER and CRT are interchangeable extensions.
Either `.cer` or `.crt` used as generic file extensions.

#### Personal Information Exchange (PFX)
This is Microsoft's certificate format.
PKCS #12 is the successor to PFX.
PFX will normally use the extension `.pfx`.
- PKCS #12 will use either `.p12` or `.pfx`