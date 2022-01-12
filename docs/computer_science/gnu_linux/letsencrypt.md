---
title: Let's Encrypt
date: 2022-01-12
author: m0wer
---

# Usage

## Request a new certificate

If there is no HTTP sever running:

```bash
certbot certonly --standalone --preferred-challenges http-01 -d {{ domain }} --register-unsafely-without-email --agree-tos -n
```

If there is an HTTP running:

```bash
certonly --webroot -w {{ web_path_letsencrypt }} --preferred-challenges http-01 -d {{ domain }} --register-unsafely-without-email --agree-tos -n
```
