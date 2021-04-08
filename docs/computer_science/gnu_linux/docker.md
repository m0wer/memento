---
title: Docker
date: 2017-10-19
tags: [ 'docker', 'virtualization', 'container', 'volumes', 'networks' ]
---

# Docker

## Usage

### Registry as a cache

`docker run -d -p 5000:5000 --restart always --name registry -e "REGISTRY_DELETE_ENABLED=true" -e "REGISTRY_PROXY_REMOTEURL=https://registry-1.docker.io" registry:2`

And the in the clients run `dockerd` with `--registry-mirror http://host:5000`.

[docker-doc](https://docs.docker.com/registry/recipes/mirror/#configure-the-docker-daemon)

### GUI

#### X server

You should mount your local *~/Xauthority* to the docker.

If it doesn't work, try from your machine:

```bash
xhost +local:root # this enables local non-network connections
```

So it enables access control.

[ros.org](http://wiki.ros.org/docker/Tutorials/GUI)

## Install

### Change docker data root path

In the `systemd` unit file:

```
ExecStart=/usr/bin/dockerd --data-root [docker_data_root_path]
```

### Manage dockers with systemd

```
[Unit]
Description=Foo Service
After=docker.service
Requires=docker.service
After=docker.redis.service
Requires=docker.redis.service

[Service]
TimeoutStartSec=0
Restart=always
ExecStartPre=-/usr/bin/docker stop foo
ExecStartPre=-/usr/bin/docker rm foo
ExecStartPre=/usr/bin/docker pull foo
ExecStart=/usr/bin/docker run --name foo
  --link docker.redi.service:redis --rm
  foo

[Install]
WantedBy=multi-user.target
```

**Note:** The “-” at the start means systemd won’t abort if the command fails.

[container-solutions](http://container-solutions.com/running-docker-containers-with-systemd/)

## Tips

### Delete dangling volumes

Delete orphan volumes (created when not running `docker run` with the `--rm` option):
`docker volume rm \`docker volume ls -q -f dangling=true\``

[coderwall](https://coderwall.com/p/hdsfpq/docker-remove-all-dangling-volumes)

### Print names in stead of IDs with `docker stats`

`docker stats $(docker ps --format '{{.Names}}')`

[stackoverflow](https://stackoverflow.com/questions/30732313/is-there-any-way-to-display-container-names-in-docker-stats)

### Get the run command of a docker

Sometimes you have a running docker of which you want to get the command line
options it was originally launched with. You can get it with:

```bash
docker run --rm -v /var/run/docker.sock:/var/run/docker.sock \
    assaflavie/runlike [container]
```

[stackoverflow](https://stackoverflow.com/questions/32758793/how-to-show-the-run-command-of-a-docker-container#answer-32774347)

### Upgrade all your currently downloaded docker images

```bash
docker images | grep -vE "(REPOSITORY|local|<none>)" | awk '{print $1":"$2}' | xargs -L1 docker pull
```

### Sort docker images by size desc

```bash
docker images --format '{{.Size}}\t{{.Repository}}\t{{.Tag}}\t{{.ID}}' | sed 's/ //' | sort -h -r | column -t
```

* [gist](https://gist.github.com/andyrbell/f30ae74c0eff82ae52238f4a7df9a313)

## Reference

### Healthcheck

* [couchbase](https://blog.couchbase.com/docker-health-check-keeping-containers-healthy/)
