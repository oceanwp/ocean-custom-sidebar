# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

Ocean Custom Sidebar is a free OceanWP add-on (on WordPress.org) that lets admins create any number of widget areas under Theme Panel > Sidebars. It only works with the OceanWP theme (or a child theme of it).

## Commands

```bash
npx grunt build          # copy a release into build/ocean-custom-sidebar/
npx grunt package        # zip build/ocean-custom-sidebar/ into build/ocean-custom-sidebar.zip
composer lint:php        # phpcs (phpcs.xml.dist) + parallel-lint + PHPCompatibilityWP 5.6+
composer make-pot        # regenerate languages/ocean-custom-sidebar.pot
composer update-mo       # merge the .pot into the es_ES and pl_PL .po files and compile .mo
```

There is no JS or CSS build (no asset files) and no npm scripts. There are no tests.

## Architecture

The whole plugin is the `Ocean_Custom_Sidebar` singleton in `ocean-custom-sidebar.php`.

- `ocs_setup()` runs on `init` and does nothing unless the active theme is OceanWP or its child. It is not gated by a license.
- Each custom sidebar is a term in the non-public taxonomy `ocean_sidebars` (term name and description). It is managed on the standard `edit-tags.php?taxonomy=ocean_sidebars` screen, added as a submenu of the Theme Panel (`oceanwp`) when Ocean Extra is active, otherwise under Appearance (`themes.php`). Small inline CSS/JS in `admin_head()` / `admin_footer()` hides the slug field and rewrites the field help text.
- On every request each term is registered with `register_sidebar()` using the ID `ocs-` + `sanitize_title( term name )`. Renaming a term changes the sidebar ID, so widgets assigned to it are no longer shown in it.
- The plugin does not choose where a sidebar appears. Ocean Extra's post metabox lists all registered widget areas for its `ocean_sidebar` / `ocean_second_sidebar` settings, and OceanWP displays the chosen one.
- The Freemius block at the bottom runs only when Ocean Extra is active (`OceanWP_EDD_Addon_Migration`), with `is_premium` and `has_paid_plans` set to false. It does not control loading.

## Coding standard

`phpcs.xml.dist`: WordPress-Extra + WordPress-Docs + PHPCompatibility (PHP 5.6+, WP 5.0+), text domain `ocean-custom-sidebar`, global prefix `ocs`.
