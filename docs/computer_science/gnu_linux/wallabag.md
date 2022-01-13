---
title: Wallabag
date: 2022-01-13
author: m0wer
---

# Installation

## NGINX reverse proxy

### Block all feeds except starred

If you want to share your Wallabag *starred* RSS feed but keep the others
(*all*, *read*...) private, add:

```nginx
location ~ /feed/sgn/{token}/(?!starred) {
   deny all;
   return 403;
  }
```
