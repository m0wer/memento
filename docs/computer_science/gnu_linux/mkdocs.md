---
title: MkDocs
date: 2021-04-15
author: m0wer
tags: [ 'mkdocs', 'markdown', 'python' ]
---

[MkDocs](https://www.mkdocs.org/) is a fast, simple and downright gorgeous
static site generator that's
geared towards building project documentation. Documentation source files are
written in Markdown, and configured with a single YAML configuration file.

# MathJax

[MathJax](https://www.mathjax.org/) is a beautiful and accessible way to
display mathematical content in the browser, allows for writing formulas in
different notations, including LaTeX, MathML and AsciiMath, and can be easily
integrated with Material for MkDocs.

## Arithmatex

[Arithmatex](https://facelessuser.github.io/pymdown-extensions/extensions/arithmatex/)
is an extension that preserves LaTeX math equations during the Markdown
conversion process so that they can be used with libraries like MathJax.

We need this extension for enabling MathJax in our site. The installation
process is as follows:

1. Edit `mkdocs.yml` and add:
  ```yaml
  markdown_extensions:
    - pymdownx.arithmatex:
        generic: true
  ```
  and
  ```yaml
  extra_javascript:
  - javascripts/config.js
  - https://polyfill.io/v3/polyfill.min.js?features=es6
  - https://cdn.jsdelivr.net/npm/mathjax@3/es5/tex-mml-chtml.js
  ```
1. Create `docs/javascripts/config.js` and add:
  ```javascript
  window.MathJax = {
    tex: {
      inlineMath: [["\\(", "\\)"]],
      displayMath: [["\\[", "\\]"]],
      processEscapes: true,
      processEnvironments: true
    },
    options: {
      ignoreHtmlClass: ".*|",
      processHtmlClass: "arithmatex"
    }
  };

  document$.subscribe(() => {
    MathJax.typesetPromise()
  })
  ```
## Usage

* Blocks must be enclosed in `$$…$$` or `\[…\]` on separate lines.
* Inline blocks must be enclosed in `$…$` or `\(…\)`.

## Reference

* [MathJax - Material for MkDocs](https://squidfunk.github.io/mkdocs-material/reference/mathjax/)

# Plugins

## mkdocs-bibtex

[shyamd/mkdocs-bibtex](https://github.com/shyamd/mkdocs-bibtex) is a plugin for
citation management using bibtex.

### Installation

Install the plugin using pip:

```
pip install mkdocs-bibtex
```

Next, add the following lines to your `mkdocs.yml`:

```yml
plugins:
  - bibtex:
      bib_file: "refs.bib"
```

### Usage

Keep your bibtex references in `refs.bib`. Then, if you want to add a reference
in an entry, cite it with `[@{cite_name}]` and add `\bibliography` wherever you
want the full references to appear.

## mkdocs-exclude-search

[chrieke/mkdocs-exclude-search](https://github.com/chrieke/mkdocs-exclude-search)
is a mkdocs plugin that lets you exclude selected chapters from the search
index.

I use it to exclude the newsletter files generated from [lyz-code/mkdocs-newsletter](https://github.com/lyz-code/mkdocs-newsletter) from the search.

### Installation

Install the plugin with

```bash
pip install mkdocs-exclude-search

```

and activate it in `mkdocs.yml` as shown in the configuration section.

### Configuration

Add the following configuration to your `mkdocs.yml`

```yaml
plugins:
  - search
  - exclude-search:
      exclude:
        - first.md
        - dir/second.md
        - third.md#some-heading
        - dir2/*
        - /*/fifth.md
      ignore:
        - dir/second.md#some-heading
```

Note that `dir/*` excludes all markdown files within a directory and its
children.

## mkdocs-newsletter

[lyz-code/mkdocs-newsletter](https://github.com/lyz-code/mkdocs-newsletter)
is a plugin that automatically creates newsletters from the changes in
a [MkDocs](mkdocs) git repository.

### Installation

You'll need to:

```bash
pip install mkdocs-newsletter
```

And enable this plugin, by changing your `mkdocs.yml`

```yaml
plugins:
  - git-revision-date-localized:
      type: timeago
  - autolinks
  - section-index
  - mkdocs-newsletter
```

## mkdocstrings

[mkdocstrings/mkdocstrings](https://github.com/mkdocstrings/mkdocstrings)
generates automatic documentation from sources.

### Configuration

```yaml
plugins:
  - mkdocstrings:
      handlers:
        python:
          setup_commands:
            - "import sys"
            - "sys.path.append('../')"
```

If we don't add `../` to the python path, the package for which we are
generating the documentation would need to be installed.

#### Automatically generate the reference files for each source file

Instead of creating manually a markdown file for every source file with
`::: package.module.file`, we can automate this with a script that will be
run automatically on every site build:

```yaml
plugins:
  - gen-files:
      scripts:
        - generate_reference.py
```

```python
from pathlib import Path
import mkdocs_gen_files

src_root = Path("../my_module")
for path in src_root.glob("**/*.py"):
    doc_path = Path("reference", path.relative_to(src_root)).with_suffix(".md")

    with mkdocs_gen_files.open(doc_path, "w") as f:
        ident = ".".join(path.with_suffix("").parts[1:])
        print("::: " + ident, file=f)
```

# Tips

## Image with caption

```markdown
<!-- markdownlint-disable MD033 -->
<figure markdown>
  ![Domain model](img/domain_model.png){ loading=lazy }
  <figcaption>Proposed model.</figcaption>
</figure>
<!-- markdownlint-enable MD033 -->
```
