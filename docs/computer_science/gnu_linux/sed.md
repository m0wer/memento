---
title: sed
date: 2017-10-18
tags: sed,vim,replace,infile,line,regexp
---
# sed

## Replace SSHd port with regexp

` sed -i 's/^Port .*/Port 77/g' /etc/ssh/sshd_config`
