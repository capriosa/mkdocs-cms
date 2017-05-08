---
title: Permalinks
date: 07.05.2017
---
Permalinks sind ein Feature der [Table of Contents][1] Erweiterung, die ein Bestandteil der Standard Markdown Bibliothek ist. Die Erweiterung fügt einen Anker an das Ende jeder Headline ein, was es möglich macht direkt auf einen bestimmten Absatz einer Seite zu verlinken.

  [1]: https://pythonhosted.org/Markdown/extensions/toc.html

## Installation

Um Permalinks zu aktivieren, füge diese Zeilen der `mkdocs.yml` hinzu:

``` yaml
markdown_extensions:
  - toc(permalink=true)
```

This will add a link containing the paragraph symbol `¶` at the end of each
headline (exactly like on the page you're currently viewing), which the
Material theme will make appear on hover. In order to change the text of the
permalink, a string can be passed, e.g.:

``` markdown
markdown_extensions:
  - toc(permalink=Link)
```

## Usage

When enabled, permalinks are inserted automatically.


