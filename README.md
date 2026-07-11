# Alchemy CMS Evaluation

This repository is a focused Rails prototype used to evaluate
[Alchemy CMS](https://alchemy-cms.com/) as a structured page-building system.
It captures a minimal host application with Alchemy mounted as its content
layer, Devise-backed editor accounts, an index page layout, and a custom
article element.

## Why this exists

The prototype explores a different CMS boundary than a conventional admin CRUD
tool. Alchemy models pages as ordered elements whose editable contents are
defined in configuration. The project was kept intentionally small so that the
page, element, essence, language, and publishing concepts could be evaluated
without unrelated product code.

This is an evaluation artifact rather than a deployed product. It documents a
technical spike and provides a compact reference for a Rails CMS integration.

## What the prototype covers

- Alchemy's page rendering and administration engines
- Devise-backed CMS users
- An `index` page layout that automatically creates its article element
- A configurable `article` element with headline, picture, and rich-text contents
- A matching article view partial and stylesheet hook
- Seeded CMS defaults, sites, and languages
- Media, attachments, tagging, page versioning, and publishing schema

## Architecture

Page structure is declared in YAML, while Rails partials control the rendered
markup. Alchemy persists each configured content slot through its element and
essence model.

```text
page layout configuration
    -> ordered Alchemy elements
    -> typed content / essence records
    -> app/views/alchemy element partials
    -> rendered page
```

For example, `config/alchemy/elements.yml` defines the article editor fields,
and `app/views/alchemy/elements/_article.html.erb` renders that structured
content. This separates the editor's content model from the presentation layer.

## Historical stack

- Ruby 2.6.1
- Rails 6.0
- Alchemy CMS with Alchemy Devise
- SQLite
- Webpacker 4 and Turbolinks 5
- Minitest

These versions are intentionally documented as historical. Ruby 2.6 and this
dependency set are no longer appropriate for a new or internet-facing
application without a deliberate upgrade and security review.

## Running the archived prototype

Use a version manager capable of installing Ruby 2.6.1, then run:

```sh
bundle install
yarn install
bin/rails db:prepare
bin/rails server
```

Open `http://localhost:3000`. The Alchemy installer migrations and seed task are
already represented in the repository.

Because the toolchain is old, installation may require an older compiler or
platform-specific dependency work. Treat upgrades as a separate modernization
project rather than silently changing the experiment's baseline.

## Verification

```sh
bin/rails test
```

The repository contains the Rails-generated test harness but no meaningful
application test coverage. If the prototype is extended, add rendering tests
for each configured element and an integration test for editor authentication
and publishing.

## What I learned

Alchemy makes the content schema explicit and keeps presentation in normal
Rails views, which is a strong fit for structured editorial pages. The tradeoff
is a larger CMS-owned persistence model and more framework vocabulary than a
simple admin interface. Building the same small experiment in isolation made
that tradeoff concrete before introducing it into a production application.
