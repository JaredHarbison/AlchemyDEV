# Alchemy Rails 6 compatibility app

This repository is a minimal Rails 6 application created in January 2020 while
investigating CMS compatibility and installation bugs.

It installs Alchemy CMS and Alchemy Devise into a newly generated Rails 6 app,
mounts the engine at the root route, and retains the generated migrations and
default article configuration. It served as a small comparison and verification
fixture alongside the Fae Rails 6 reproduction—not as a standalone CMS product.

## Compatibility context

- Ruby 2.6.1
- Rails 6.0.2
- Alchemy CMS 4.x
- Alchemy Devise
- SQLite

The initial commits preserve the complete setup sequence:

1. Generate a Rails 6 application.
2. Add `alchemy_cms` and `alchemy-devise`.
3. Mount `Alchemy::Engine` at `/`.
4. Run `alchemy:install` and the Alchemy Devise installer.
5. Retain the generated schema, seed data, page layout, and article element.

## Historical status

This is an archived compatibility fixture with an intentionally old dependency
lockfile. It should not be deployed or used as the starting point for a new
application. The open dependency alerts reflect the age of the fixture rather
than an actively maintained product.
