---
title: GPG
date: 2019-06-20
tags: [ 'gpg', 'pgp', 'key', 'rsa', 'privacy' ]
---

# GPG

## Usage

### Generate a key

Use `gpg --gen-key` or `gpg --full-gen-key` for more options.

### Export a key

#### Export public key

```bash
gpg --output public.pgp --armor --export username@email
```

## Reference

### Usage

* [easyengine.io](https://easyengine.io/tutorials/linux/gpg-keys/) General
  commands.

### Keyservers

* [sks-keyservers](https://sks-keyservers.net/status/) List of SKS servers in
  the pool.

#### SKS keyservers

* [urown.net](https://pgpkeys.urown.net:11371/) with
  [.onion](http://pgpkeysximvxiazm.onion/) and IPv6.
