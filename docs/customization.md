---
title: Anpassungen
date: 07.05.2017
---
## Ein guter Ausgangspunkt

Projekt Dokumentationen sind so vielfältig wie die Projekte selbst. Das Material Theme ist ein guter Ausgangspunkt damit die Dokumentationen schön aussehen. Aber manchmal wird es notwendig sein kleine Anpassungen vorzunehmen, um eigene Vorstellungen was das Design betrifft umzusetzen.

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

## Extending the theme

If you want to alter the HTML source (e.g. add or remove some part), you can
extend the theme. From version 0.16 on MkDocs implements [theme extension](http://www.mkdocs.org/user-guide/styling-your-docs/#using-the-theme_dir),
an easy way to override parts of a theme without forking and changing the
main theme.

### Setup and theme structure

Reference the Material theme as usual in your `mkdocs.yml`, and create a
new folder for overrides, e.g. `theme`, which you reference using `theme_dir`:

    theme: 'material'
    theme_dir: 'theme'

!!! warning "Theme extension prerequisites"

    As the `theme_dir` variable is used for the theme extension process, the
    Material theme needs to be installed via `pip` and referenced with the
    `theme` parameter in your `mkdocs.yml`.

The structure in the theme directory must mirror the directory structure of the
original theme, as any file in the theme directory will replace the file with
the same name which is part of the original theme. Besides, further assets
may also be put in the theme directory.

The directory layout of the Material theme is as follows:

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

### Overriding partials

In order to override the footer, we can replace the `footer.html` partial with
our own partial. To do this, create the file `partials/footer.html` in the
theme directory. MkDocs will now use the new partial when rendering the theme.
This can be done with any file.

### Overriding template blocks

Besides overriding partials, one can also override so called template blocks,
which are defined inside the Material theme and wrap specific features. To
override a template block, create a `main.html` inside the theme directory and
define the block, e.g.:

    {% extends "base.html" %}
    
    {% block htmltitle %}
      <title>Lorem ipsum dolor sit amet</title>
    {% endblock %}

The Material theme provides the following template blocks:

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

For more on this topic refer to the [MkDocs documentation](http://www.mkdocs.org/user-guide/styling-your-docs/#overriding-template-blocks)

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

