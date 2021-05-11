---
title: LaTeX
date: 2018-06-21
tags: [ 'latex', 'tex', 'pdflatex', 'math', 'science' ]
---

# Cheatsheet

## Style

Use point as the decimal separator: `\decimalpoint`.

[stackexchange](https://tex.stackexchange.com/questions/82009/babel-and-the-decimal-separator)

## Greek letters

* epsilon: **\varepsilon** $ \varepsilon $
* rho: **\rho** $ \rho $
* phi: **\phi** $ \phi $

Not greek, but related:

* Nabla: **\nabla** $ \nabla $

[uib](http://web.ift.uib.no/Teori/KURS/WRK/TeX/sym1.html)
[wikipedia](https://en.wikipedia.org/wiki/Greek_alphabet)

## Math

### Vectors

* Unit vectors: **\hat{v}** $ \hat{v} $

### Integrals

* Triple integrals: **\iiint xyz dxdydz** $ \iiint xyz dxdydz $

#### Closed integrals

Using packages **asmath** and **esint**.

* **\oiint** $ \oiint $

[stackexchange-tex](https://tex.stackexchange.com/questions/134416/surface-integral)

## Quotation

To quote some text you can't directly use "", you should wrap it around `` and
'' instead.

* [stackexchange](https://tex.stackexchange.com/questions/64371/direct-quotations-and-entire-paragraph-quotations)

## Rename tables names in Spanish

By default, the caption of a table will start with “Cuadro: ” when using
`\usepackage[spanish]{babel}`. if you want to change it to something else, for
example “Tabla: ” add the following lines after `\begin{document}`:

```latex
% Cambiar Cuadros por Tablas y lista de...
\renewcommand{\listtablename}{Índice de tablas}
\renewcommand{\tablename}{Tabla}
```

# Usage

## Plugins

### Minted

#### Import code from file

```tex
\inputminted{<lang>}{<file>}
```

* [stackexchange](https://tex.stackexchange.com/questions/44018/how-do-i-import-a-source-file-using-minted)

## Figures

### Tips

* To ensure figures appear before certain point, use
  [placeins](https://ctan.org/pkg/placeins). For example:

  ```latex
  \usepackage[section]{placeins}

  % ... some floats here ...

  \FloatBarrier
  ```

# Reference

## Packages

* [ConTeXt](https://tex.stackexchange.com/questions/2099/how-to-include-svg-diagrams-in-latex)
   To include **.svg** diagrams directly.
* [minted](https://github.com/gpoore/minted) To enable syntax highlighting,
  supports VHDL.
* [TikZ](https://github.com/pgf-tikz/pgf) A Portable Graphic Format for TeX
