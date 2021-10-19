---
title: nginx
date: 2017-10-26
tags: [ 'nginx', 'web', 'server' ]
---

# Configuration

## Serve static files

Either

```
location /static/ {
    root /var/www/app/;
}
```

or

```
location /static/ {
    alias /var/www/app/static/;
}
```

The difference is that with `alias` the location part gets dropped from the
original URL so `http://host/static/somefile` would access
`/var/www/app/static/somefile` instead of
`/var/www/app/static/somefile/somefile`.

## Reverse proxy

In the vhost file, add

```
location /something/ {
    proxy_pass http://127.0.0.1:8000/;  # note the trailing slash here, it matters!
}
```

## Disable showing nginx's version in the error pages

`server_tokens off;`

[scalescale](https://www.scalescale.com/tips/nginx/how-to-hide-nginx-version/)
