---
title: OpenLDAP
date: 2019-06-13
tags: [ 'openldap', 'ldap', 'uid' ]
---

# Usage

## Don't check certs

```bash
LDAPTLS_REQCERT=never [command]
```

Or add `TLS_REQCERT never` to `/etc/openldap/ldap.conf`.

# Tips

## Get highest uidNUmber on LDAP

```bash
ldapsearch -H ldaps://your-ldap-domain -D "cn=Manager,dc=domain,dc=com" -W | awk '/uidNumber: / {print $2}' | sort | tail -n 1
```
