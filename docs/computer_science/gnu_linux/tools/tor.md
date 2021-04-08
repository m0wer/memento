---
title: TOR
date: 2019-06-21
tags: [ 'tor', 'onion', 'routing', 'privacy' ]
---

# TOR

## Configuration

### Hidden services

1. Enable `HiddenServiceDir` and at least one `HiddenServicePort` in
   */etc/tor/torrc*.
1. Then create the `HiddenServiceDir` and give it the proper permissions, for
   example:
   ```bash
   mkdir /var/lib/tor/hidden_service/
   chown debian-tor:debian-tor /var/lib/tor/hidden_service/
   chmod 0700 /var/lib/tor/hidden_service/
   ```
1. Restart the `tor` service.

You can get the hostname (.onion) from *`HiddenServiceDir`/hostname*.

* [medium.com](https://medium.com/@ajphillips/how-to-create-your-own-tor-hidden-service-436bece8602f)

#### Custom onion hostname

To get a customized .onion url you can use
[Shallot](https://github.com/katmagic/Shallot).

## Debug

### Check if Tor is working from the command line

```bash
curl --socks5 localhost:9050 --socks5-hostname localhost:9050 -s https://check.torproject.org/ | cat | grep -m 1 Congratulations | xargs

```

* [stackexchange](https://tor.stackexchange.com/questions/12678/how-to-check-if-tor-is-working-and-debug-the-problem-on-cli)
