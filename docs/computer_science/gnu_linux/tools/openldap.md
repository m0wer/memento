---
title: OpenLDAP
date: 2019-06-13
tags: [ 'openldap', 'ldap', 'uid' ]
---

# OpenLDAP

## Usage

### Don't check certs

```bash
LDAPTLS_REQCERT=never [command]
```

* [serverfault](https://serverfault.com/questions/398684/ubuntu-12-04-ldap-ssl-self-signed-cert-not-accepted)

## Tips

### Get highest uidNUmber on LDAP

```bash
ldapsearch -H ldaps://your-ldap-domain -D "cn=Manager,dc=domain,dc=com" -W | awk '/uidNumber: / {print $2}' | sort | tail -n 1
```

* [dynobin](https://www.dynobin.com/linux-find-max-uidnumber-on-ldap/)
