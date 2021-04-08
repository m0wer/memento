---
title: elogind
date: 2020-04-15
tags: [ 'elogind' ]
---

# elogind

## Configuration

### Lock screen and suspend

```bash
#!/bin/sh
#
# /lib/elogind/system-sleep/lock.sh
# Lock before suspend integration with elogind

username=lerax
userhome=/home/$username
export XAUTHORITY="$userhome/.Xauthority"
export DISPLAY=":0.0"

case "${1}" in
        pre)
            su $username -c "/usr/bin/slock" &
            sleep 1s;
            ;;
esac
```

* [How lock your system before suspend with openrc init via elogind using slock](https://gist.github.com/ryukinix/bd0c1ddcbbafdb4149ae70e41b7c822b)
