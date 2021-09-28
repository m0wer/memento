---
title: netcat
date: 2017-10-26
tags: [ 'netcat', 'net', 'bind', 'port', 'scan', 'usage', 'reference', 'options' ]
---

# Usage

## Test TCP connections

```bash
nc -v -z -w 3 [host] [port]
```

Options:
  * `-v`: verbose
  * `-z`: just check if the port is open and exit (without sending any data)
  * `-w 3`: 3 seconds timeout

If it exists with return code 0, it means that the connection succeeded.

## Listen to a port

`netcat -l [port]`

## Scan port range

`nc -zvnw 1 [ip] 1-1000`

* `-z` Port scanning mode.
* `-v` Verbose.
* `-n` Do not resolve the host name.
* `-w 1` 1s timeout.

[cybercity](https://www.cyberciti.biz/faq/linux-port-scanning/)

## Connect through TOR

```bash
nc -v -X5 -x localhost:9050 [server] [port]
```

* [vicendominguez](http://vicendominguez.blogspot.com/2014/08/using-nc-and-ncat-with-tor-without.html)

# Reference

## Basic usage

* [digitalocean](https://www.digitalocean.com/community/tutorials/how-to-use-netcat-to-establish-and-test-tcp-and-udp-connections-on-a-vps)
