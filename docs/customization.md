---
title: Anpassungen
date: 07.05.2017
---
## Ein guter Ausgangspunkt

Projekt Dokumentationen sind so vielfältig wie die Projekte selbst. Das Material Theme ist ein guter Ausgangspunkt damit die Dokumentationen schön aussehen. Aber manchmal wird es notwendig sein kleine Anpassungen vorzunehmen, um eigene Vorstellungen, was das Design betrifft, umzusetzen.

## Assets hinzufügen

[MkDocs](http://www.mkdocs.org) bietet verschiedene Möglichkeiten Themes anzupassen. Hierzu fügst du einfach dem `docs` Verzeichnis Stylesheet oder Javascript Dateien hinzu.

### Zusätzliche Stylesheets

Zusätzliche Styleseehts werden am Besten in einem Unterverzeichnis des `docs` Verzeichnis hinzugefügt:

    mkdir docs/stylesheets
    touch docs/stylesheets/extra.css

Danach müssen folgende Zeilen der `mkdocs.yml hinzugefügt werden`:

    extra_css:
      - 'stylesheets/extra.css'

Nach dem Start des lokalen Entwicklungs-Server mit `mkdocs serve` werden Änderungen der Stylesheets dank \*live reloading\* sofort im Browser angezeigt.

### Zusätzliches JavaScript

Das gleiche gilt für JavaScript. Auch zusätzliche JavaScript Dateien sollten in einem Unterverzeichnis des `docs` Verzeichnis gespeichert werden:

    mkdir docs/javascripts
    touch docs/javascripts/extra.js

Danach müssen folgende Zeilen der `mkdocs.yml hinzugefügt werden`:

    extra_javascript:
      - 'javascripts/extra.js'

Weitere Hilfe ist in der [MkDocs Dokumentation](http://www.mkdocs.org/user-guide/styling-your-docs/#customizing-a-theme) zu finden.

## Das Theme erweitern

Um das HTML des Themes zu ändern, sollte folgendermaßen vorgegangen werden. Seit Version 0.16 implementiert MkDocs [theme extension](http://www.mkdocs.org/user-guide/styling-your-docs/#using-the-theme_dir),
eine einfache Möglichkeit, um Teile von Themes zu ändern ohne das Original-Theme zu komprimitieren.

### Setup und Theme-Struktur

Referenziere das Material Theme wie gewöhnlich in der `mkdocs.yml`, erzeuge ein neues Verzeichnis, z.B. `theme`, welches du dann mit dem `key:` `theme_dir` referenzierst:

    theme: 'material'
    theme_dir: 'theme'

!!! warning "Voraussetzungen für Theme-Erweiterungen"

    Da die `theme_dir` Variable vom Theme-Erweiterungsprozess, muss
    das Material Theme mit `pip` installiert werden.

Die Struktur des neues Theme Verzeichnis muss dem des
Original Theme entsprechen, da jede Datei in diesem Verzeichnis, eine Datei mit dem gleichen Namen im Original-Theme ersetzen wird. Zusätzliche Dateien können dem neuen Verzeichnis jedoch hinzugefügt werden..

Die Verzeichnisstruktur des Material Theme ist wir folgt:

    .
    ├─ assets/
    │  ├─ images/                          # Images and icons
    │  ├─ javascripts/                     # JavaScript
    │  └─ stylesheets/                     # Stylesheets
    ├─ partials/
    │  ├─ disqus.html                      # Disqus integration
    │  ├─ footer.html                      # Footer bar
    │  ├─ header.html                      # Header bar
    │  ├─ language.html                    # Localized labels
    │  ├─ nav-item.html                    # Main navigation item
    │  ├─ nav.html                         # Main navigation
    │  ├─ search.html                      # Search box
    │  ├─ social.html                      # Social links
    │  ├─ source.html                      # Repository information
    │  ├─ tabs-item.html                   # Tabs navigation item
    │  ├─ tabs.html                        # Tabs navigation
    │  ├─ toc-item.html                    # Table of contents item
    │  └─ toc.html                         # Table of contents
    ├─ 404.html                            # 404 error page
    ├─ base.html                           # Base template
    └─ main.html                           # Default page

### Partials überschreiben

Um z.B. den Footer zu verändern, kann einfach das `footer.html` Partial durch eine eigene `footer.html`im neuen Theme-Verzeichnis ersetzt werden. MkDocs benutzt dann das neue Partial, wenn das Theme gerendert wird. Dies gilt für jede Datei.

### Template Blöcke überschreiben

Neben Partials können auch sog. Template-Blöcke überschrieben werden, 
die sich auch im Material Theme befinden und spezielle *Features* zur Verfügung stellen. Um einen Template-Block zu überschreiben, erzeuge eine `main.html` im Theme-Verzeichnis und definiere den Block, z.B.:

    {% extends "base.html" %}
    
    {% block htmltitle %}
      <title>Lorem ipsum dolor sit amet</title>
    {% endblock %}

Das Material Theme stellt folgende Template Blöcke zur Verfügun:

| Block name   | Wrapped contents                                |
| ------------ | ----------------------------------------------- |
| `analytics`  | Wraps the Google Analytics integration          |
| `content`    | Wraps the main content                          |
| `disqus`     | Wraps the disqus integration                    |
| `extrahead`  | Empty block to define additional meta tags      |
| `fonts`      | Wraps the webfont definitions                   |
| `footer`     | Wraps the footer with navigation and copyright  |
| `header`     | Wraps the fixed header bar                      |
| `htmltitle`  | Wraps the `<title>` tag                         |
| `libs`       | Wraps the JavaScript libraries, e.g. Modernizr  |
| `repo`       | Wraps the repository link in the header bar     |
| `scripts`    | Wraps the JavaScript application logic          |
| `source`     | Wraps the linked source files                   |
| `search_box` | Wraps the search form in the header bar         |
| `site_meta`  | Wraps the meta tags in the document head        |
| `site_name`  | Wraps the site name in the header bar           |
| `site_nav`   | Wraps the site navigation and table of contents |
| `social`     | Wraps the social links in the footer            |
| `styles`     | Wraps the stylesheets (also extra sources)      |

Mehr Informationen zu diesem Thema sind hier zu finden: [MkDocs documentation](http://www.mkdocs.org/user-guide/styling-your-docs/#overriding-template-blocks)

## Theme development

The Material theme is built on modern technologies like ES6, [Webpack](https://webpack.github.io/),
[Babel](https://babeljs.io) and [SASS](http://sass-lang.com). If you want to make more fundamental changes, it may
be necessary to make the adjustments directly in the source of the Material
theme and recompile it. This is fairly easy.

### Environment setup

In order to start development on the Material theme, a [Node.js](https://nodejs.org) version of
at least 5 is required, as well as the package manager [yarn](https://yarnpkg.com/) which is a
better version of `npm`. First, clone the repository:

    git clone https://github.com/squidfunk/mkdocs-material

Next, all dependencies need to be installed, which is done with:

    cd mkdocs-material
    pip install -r requirements.txt
    yarn install

### Development mode

The Material theme uses a sophisticated asset pipeline using [Gulp](http://gulpjs.com) and
Webpack which can be started with the following command:

    yarn start

This will also start the MkDocs development server which will monitor changes
on assets, templates and documentation. Point your browser to
[localhost:8000](http://localhost:8000) and you should see this documentation in front of you.

For example, changing the color palette is as simple as changing the
`$md-color-primary` and `$md-color-accent` variables in
`src/assets/stylesheets/_config.scss`:

    $md-color-primary: $clr-red-400;
    $md-color-accent:  $clr-teal-a700;

!!! warning "Automatically generated files"

    Never make any changes in the `material` directory, as the contents of this
    directory are automatically generated from the `src` directory and will be
    overriden when the theme is built.

### Build process

When you've finished making your changes, you can build the theme by invoking:

    yarn run build

This triggers the production-level compilation and minification of all
stylesheets and JavaScript sources. When the command exits, the final theme is
located in the `material` directory. Add the `theme_dir` variable pointing to
the aforementioned directory in your original `mkdocs.yml`.

Now you can run `mkdocs build` and you should see your documentation with your
changes to the original Material theme.



