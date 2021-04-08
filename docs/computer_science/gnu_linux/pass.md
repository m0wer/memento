---
title: Pass: the standard unix password manager
date: 2019-10-08
tags: [ 'pass', 'passwordstore', 'unix' ]
---

# Pass: the standard unix password manager

## Usage

### Re-encrypt *.password-store* using new gpg key

```bash
pass init -p <path> <gpg-id(s)>
```

Specify the `<path>` relative to *~/.password-store*.

* [askubuntu](https://askubuntu.com/questions/929307/how-to-change-the-gpg-key-of-the-pass-password-store)

## Reference

* <https://www.passwordstore.org/>
* [medium.com](https://medium.com/@davidpiegza/using-pass-in-a-team-1aa7adf36592)
