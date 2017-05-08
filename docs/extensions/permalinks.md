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

Dadurch wird ein Link mit diesem Symbol `¶` an das Ende jeder Headline hinzugefügt. (So wie es hier auf dieser Seite zu sehen ist)

Um den Text der Permalinks zu ändern, muss der Konfiguration ein Text hinzugefügt werden, z.B.:

``` markdown
markdown_extensions:
  - toc(permalink=Link)
```

## Anwendung

Wenn die Erweiterung aktiviert ist, werden Permalinks automatisch hinzugefügt.



