---
title: Telegraf: metrics collector
date: 2019-09-07
tags: [ 'telegraf', 'grafana', 'influxdb', 'metrics' ]
---

# Telegraf: metrics collector

## Install

For Debian 9 Stretch:

```bash
cat <<EOF | sudo tee /etc/apt/sources.list.d/influxdata.list
deb https://repos.influxdata.com/debian stretch stable
EOF
curl -sL https://repos.influxdata.com/influxdb.key | apt-key add -
apt update && apt install telegraf -y
systemctl enable --now telegraf
```

* [computingforgeeks](https://computingforgeeks.com/how-to-install-and-configure-telegraf-on-ubuntu-18-04-debian-9/)

## Config

### Docker

```bash
usermod -a -G docker telegraf
```

### Nginx logparser

```bash
usermod -a -G adm telegraf
```

### Nginx status

Enable `stub_status`:

```
location /nginx_status {
   stub_status on;
   allow 127.0.0.1;        #only allow requests from localhost
   deny all;               #deny all other hosts
}
```

### Smartctl

Install `smartmontools` and add with `visudo` the following lines:

```
# Monitoring tool
telegraf  ALL=(ALL) NOPASSWD: /usr/sbin/smartctl
```
