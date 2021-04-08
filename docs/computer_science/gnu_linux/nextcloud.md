---
title: Nextcloud debug and troubleshooting
date: 2018-10-15
tags: [ 'nextcloud', 'owncloud', 'slow', 'performance' ]
---

# Nextcloud

## Debug

### Extremely slow

#### Website takes a long time to load, desktop and mobile apps stop working

This might be happening because the host of a shared folder can't be reached.
You can try to delete those folders via the web interface. If it doesn't work,
try login to the database and removing the external shared folders table with:

```sql
delete from oc_share_external;
```

[nextcloud help](https://help.nextcloud.com/t/cant-get-my-nextcloud-desktop-client-to-sync-again-after-updating-from-12-0-0-to-12-0-1-login-to-nc-very-slow-after-update/19186/15)
[github issue](https://github.com/nextcloud/server/pull/5753)

### Can't login from apps

If the Nextcloud instance is behind a reverse proxy, maybe you should add the
`overwriteportocol` directive to the server config.

[bayton](https://bayton.org/docs/nextcloud/nexcloud-behind-a-proxy-fixing-mixed-content-warnings-with-ssl/)
