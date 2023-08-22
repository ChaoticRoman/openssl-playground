# OpenSSL playground

## Generate RSA private key
```
openssl genrsa -out test.key 4096
```
## Generate corresponding private key
```
openssl rsa -pubout -in test.key -out test.pub.key
```
## Create a file, sign it and save the signature in base64 format
```
echo Hello > document.txt
openssl dgst -sha256 -sign test.key -out signature.sha256 document.txt
openssl base64 -in signature.sha256 -out signature.sha256.base64
```
