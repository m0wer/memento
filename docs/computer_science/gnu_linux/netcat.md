---
title: netcat
date: 2017-10-26
tags: [ 'netcat', 'net', 'bind', 'port', 'scan', 'usage', 'reference', 'options' ]
---

# netcat

## Usage

### Listen to a port

`netcat -l [port]`

### Scan port range

`nc -zvnw 1 [ip] 1-1000`

* `-z` Port scanning mode.
* `-v` Verbose.
* `-n` Do not resolve the host name.
* `-w 1` 1s timeout.

[cybercity](https://www.cyberciti.biz/faq/linux-port-scanning/)

### Connect through TOR

```bash
nc -v -X5 -x localhost:9050 [server] [port]
```

* [vicendominguez](http://vicendominguez.blogspot.com/2014/08/using-nc-and-ncat-with-tor-without.html)

## Reference

### Basic usage

* [digitalocean](https://www.digitalocean.com/community/tutorials/how-to-use-netcat-to-establish-and-test-tcp-and-udp-connections-on-a-vps)
