---
title: 'Ein CMS, mit Material Design, für Dokumentationen'
date: 08.05.2017
---
## Wünderschöne Dokumentationen

Material ist ein Theme für [MkDocs](http://www.mkdocs.org), ein ausgezeichneter Static Site Generator für Online-Dokumentationen. Das Design basiert auf Google's [Material Design](https://www.google.com/design/spec/material-design)
Richtlinien.

!!! summary "MkDocs mit CMS"

Ich habe das [Netlify-CMS](https://netlifycms.org) 
mit MkDocs und dem Material Theme verknüpft. Wenn 
du einen Github und Netlify Account hast, kannst du 
alles mit einem Klick [deployen](https://app.netlify.com/start/deploy?
repository=https://github.com/capriosa/mkdocs-cms) 
und deine Dokumentationen bequem *On-Site* mit einem CMS erstellen.

Bitte, lies vorher [hier den Abschnitt über Authenticate with Github](https://www.netlifycms.org/docs/test-drive/).

[![Material für MkDocs](images/material.png)](images/material.png)

## Start

Installation der neuesten Version von Material mit `pip`:

    pip install mkdocs-material

Füge diese Zeile der Datei `mkdocs.yml` im Root von Material hinzu:

    theme: 'material'

Weitere detaillierte Instruktionen sind hier [getting started guide](getting-started.md) zu finden.

