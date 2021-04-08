---
title: Firefox
date: 2018-11-02
tags: [ 'firefox', 'browser', 'them', 'gtk', 'debug', 'fix', 'tips', 'usage', 'config', 'reference' ]
---

# Firefox

## Debug

### Input black background

Firefox messes up every input if the GTK theme is dark. There are a lot of
workarounds.

* [Text Contrast
  Plugin](https://addons.mozilla.org/en-US/firefox/addon/text-contrast-for-dark-themes/)
* Use a light theme for firefox
  [archlinux-wiki](https://wiki.archlinux.org/index.php/firefox#Dark_themes)

### Some file types won't display and directly open the download popup instead

This happened to me when trying to use the
[markdown-viewer](https://github.com/KeithLRobertson/markdown-viewer) plugin.
To fix this, add a new MIME type in
*~/.local/share/mime/packages/text-markdown.xml*:

```xml
<?xml version="1.0"?>
<mime-info xmlns='http://www.freedesktop.org/standards/shared-mime-info'>
  <mime-type type="text/plain">
    <glob pattern="*.md"/>
    <glob pattern="*.mkd"/>
    <glob pattern="*.markdown"/>
  </mime-type>
</mime-info>
```

And then run `update-mime-database ~/.local/share/mime`.

### Encoding error for local files

Set UTF-8 as fallback in [about:config](about:config):
`intl.charset.fallback.utf8_for_file` = `true`.

[markdown-viewer](https://github.com/KeithLRobertson/markdown-viewer)

## Reference

### Plugins

* [markdown-viewer](https://github.com/KeithLRobertson/markdown-viewer)
