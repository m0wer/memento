---
title: iptables
date: 2017-10-26
tags: [ 'iptables', 'ufw', 'firewall', 'clear', 'rules', 'netfilter', 'usage', 'delete' ]
---

# iptables

## Usage

### Allow from range from an interface to an specific port

`iptables -A INPUT -p tcp -i [interface] -s [range] --dport [port] -j ACCEPT`

[serverfault](https://serverfault.com/questions/161401/how-to-allow-a-range-of-ips-with-iptables)

## Install

### iptables-persistent

When installed, it will save the current rules. If you want to save more
afterwards, you have to manually save them:

`iptables-save >/etc/iptables/rules.v4`

[stackexchange-unix](https://unix.stackexchange.com/questions/125833/why-isnt-the-iptables-persistent-service-saving-my-changes)

## Tips

### Clear all rules and allow all traffic

```bash
iptables -F
iptables -X
iptables -t nat -F
iptables -t nat -X
iptables -t mangle -F
iptables -t mangle -X
iptables -P INPUT ACCEPT
iptables -P FORWARD ACCEPT
iptables -P OUTPUT ACCEPT
```

[adminsehow](https://www.adminsehow.com/2009/08/how-to-clear-all-iptables-rules/)
