---
title: Pandoc
date: 2019-10-10
tags: [ 'pandoc', 'pdf', 'latex' ]
---

# Pandoc

## Usage

### Download website to LaTeX PDF

```bash
pandoc --pdf-engine=xelatex -s -r html [url] -o out.pdf
```
