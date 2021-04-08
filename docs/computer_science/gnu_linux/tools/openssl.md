---
title: OpenSSL usage guide
date: 20180925
tags: openssl,ssl,https,certificates,RSA,csr,key
---

# OpenSSL usage guide

## Key

### Generate a RSA key

`openssl genrsa -out [key file] [bit size]`

**[bit size]**: 2048, 4096...

## CSR

### Get information from a CSR file

`openssl req -in [csr file] -text -noout`

[shellhacks](https://www.shellhacks.com/decode-csr/)

### Generate a CSR

1. Generate a key file.
2. Create a *csr.conf* file (recommended) with the following contents:

```
[ req ]
default_bits       = [key bit size]
default_md         = sha512
default_keyfile    = [domain]
prompt             = no
encrypt_key        = no
distinguished_name = req_distinguished_name
# distinguished_name
[ req_distinguished_name ]
countryName            = "[C]"                     	# C=
localityName           = "[L]"                 		# L=
organizationName       = "[O]"             			# O=
organizationalUnitName = "[OU]"            			# OU=
commonName             = "[CN]"           			# CN=
emailAddress           = "[CN/emailAddress]"		# CN/emailAddress=
```
3. Generate de CSR file for the key:
`openssl req -config csr.conf -new  -key [key file] -out [CSR file] -verbose`

[medium](https://medium.com/curiouscaloo/how-to-generate-a-wildcard-cert-csr-with-a-config-file-for-openssl-8a6613ab342f)
