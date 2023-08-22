# OpenSSL playground

## Generate RSA private key
```
openssl genrsa -out test.key 4096
```
## Generate corresponding private key
```
openssl rsa -pubout -in test.key -out test.pub.key
```
