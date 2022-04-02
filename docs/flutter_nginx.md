h---
title: Flutter NGINX configuration
date: 2022-02-12
author: m0wer
---

# Configuration

## Support named routes

To support named routes (e.g., `APP_HOST/some/route`), add the following
configuration to the host configuration file:

```nginx
location / {
    try_files $uri $uri/ /index.html;
}
```

Otherwise NGINX will return 404 when queried for a named route since the
corresponding file won't exist in the root directory.
