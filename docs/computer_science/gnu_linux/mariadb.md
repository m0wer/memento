---
title: MariaDB
date: 2021-09-05
author: m0wer
tags: [ 'SQL' ]
---

# Tips

## Gain root access without the password

This can be useful for resetting the password or just for performing privileged
actions without entering the root password.

Start the database in the background without loading the grant tables or
enabling networking:

```bash
mysqld_safe --skip-grant-tables --skip-networking &
```

Then access it with:

```bash
mysql -u root
```
