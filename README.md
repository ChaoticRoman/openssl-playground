# OpenSSL playground

## Generate RSA private key
```
openssl genrsa -out private.pem 4096
```

Keep the private key safe and secret!

You can also protect your private key with passphrase to enhance security,
on the other hand it makes harder automated usage:

```
openssl genrsa -aes128 -out private.pem 4096
```

## Generate corresponding public key
```
openssl rsa -pubout -in private.pem -out public.pem
```
The public key can be regenerated and is intended to be publicly distributed.

## Create a file, sign it using your private key and save the signature in base64 format
```
echo Hello > document.txt
openssl dgst -sha256 -sign private.pem -out signature.sha256 document.txt
openssl base64 -in signature.sha256 -out signature.sha256.base64
```

## Decode the signature and verify the file using your public key
```
openssl base64 -d -in signature.sha256.base64 -out signature-out.sha256
openssl dgst -sha256 -verify public.pem -signature signature-out.sha256 document.txt
```

## Try to tamper with the file and try again
```
echo Hello1 > document.txt
openssl dgst -sha256 -verify public.pem -signature signature-out.sha256 document.txt
```

## Restore and check again
```
echo Hello > document.txt
openssl dgst -sha256 -verify public.pem -signature signature-out.sha256 document.txt
```

## Encrypting and decrypting the document using asymmetric encryption

```

```

## References

* https://opensource.com/article/21/4/encryption-decryption-openssl
