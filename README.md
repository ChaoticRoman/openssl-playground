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
## Decode the signature and verify the file
```
openssl base64 -d -in signature.sha256.base64 -out signature-out.sha256
openssl dgst -sha256 -verify test.pub.key -signature signature-out.sha256 document.txt
```
## Try to tamper with the file and try again
```
echo Hello1 > document.txt
openssl dgst -sha256 -verify test.pub.key -signature signature-out.sha256 document.txt
```
## Restore and check again
```
echo Hello > document.txt
openssl dgst -sha256 -verify test.pub.key -signature signature-out.sha256 document.txt
```
