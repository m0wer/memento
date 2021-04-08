---
title: dig usage guide
date: 2018-10-23
tags: [ 'dig', 'dns', 'lookup', 'nameserver', 'domain', 'soa' ]
---

# dig usage guide

## Get primary DNS server for a given domain

`dig [domain] soa +short`

[stackoverflow](https://unix.stackexchange.com/questions/165946/how-to-get-primary-dns-server-ip-of-specific-domain)

## Get CAA register for a given domain

`dig caa [domain]`

[stackoverflow](https://security.stackexchange.com/questions/168133/how-can-i-look-up-a-certificate-authorities-caa-record-value)
