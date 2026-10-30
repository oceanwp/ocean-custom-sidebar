# Ocean Custom Sidebar - Features Documentation

Complete documentation of all features available in Ocean Custom Sidebar.

---

## Table of Contents

1. [Plugin Overview](#plugin-overview)
2. [License & Availability](#license--availability)
3. [Custom Sidebars](#custom-sidebars)
4. [Assigning a Sidebar to a Page](#assigning-a-sidebar-to-a-page)
5. [Admin Pages](#admin-pages)
6. [Display & Developer API](#display--developer-api)

---

## Plugin Overview

**Ocean Custom Sidebar** lets you create any number of extra widget areas for the OceanWP theme and use them on the pages you choose.

| Property | Value |
|----------|-------|
| Version | 1.1.6 |
| Minimum WordPress | 5.6 |
| Tested up to | 7.1 |
| Text Domain | `ocean-custom-sidebar` |
| Main class | `Ocean_Custom_Sidebar` (singleton, `Ocean_Custom_Sidebar()`) |
| Requires | OceanWP theme (or a child theme). Ocean Extra is needed to pick a sidebar per page |
| Distribution | Free on WordPress.org |

### Key Capabilities

- Create unlimited sidebars with a name and an optional description
- Each sidebar becomes a normal widget area in **Appearance > Widgets**
- Use a custom sidebar on any post or page through the OceanWP Settings metabox
- Translations included for Spanish and Polish

---

## License & Availability

Ocean Custom Sidebar is free. It registers with Freemius (product ID `3810`) only when Ocean Extra is active, as a free product with no paid plans. All features work without a license.

---

## Custom Sidebars

Go to **OceanWP > Sidebars** (or **Appearance > Sidebars** when Ocean Extra is not active) to add, edit and delete sidebars. The screen is the standard WordPress term screen, with the slug field hidden.

| Field | Description | Default |
|-------|-------------|---------|
| **Name** | The name of the widget area | Required |
| **Description** | Optional description of the widget area | Empty |

The list table shows **Name**, **ID** and **Description**. The ID column is sortable.

Each sidebar is registered on every page load with:

| Property | Value |
|----------|-------|
| ID | `ocs-` + the sanitized sidebar name (for example "Shop Sidebar" becomes `ocs-shop-sidebar`) |
| Widget wrapper | `<div class="sidebar-box {widget-class} clr">` |
| Widget title | `<h4 class="widget-title">` |

The ID is built from the name, so renaming a sidebar gives it a new ID. Widgets placed in it under the old ID no longer show in it.

---

## Assigning a Sidebar to a Page

The plugin only creates the widget areas. To use one, edit a post or page and pick it in the **Sidebar** or **Second Sidebar** setting of Ocean Extra's OceanWP Settings metabox. That list includes every registered widget area, so custom sidebars appear there next to the theme's own. OceanWP then shows the chosen sidebar on that page.

---

## Admin Pages

| Screen | Location | Purpose |
|--------|----------|---------|
| Sidebars | **OceanWP > Sidebars** with Ocean Extra, otherwise **Appearance > Sidebars** | Create and manage custom sidebars (needs `manage_options`) |

---

## Display & Developer API

### Filters

| Hook | Description |
|------|-------------|
| `ocean_taxonomy_objects_sidebars` | Object types the `ocean_sidebars` taxonomy is attached to (default none) |
| `ocean_taxonomy_args_sidebars` | Arguments for the `ocean_sidebars` taxonomy |

### Data Storage

| Data | Where |
|------|-------|
| Sidebars | Terms of the non-public taxonomy `ocean_sidebars` (name and description) |
| Version | Option `ocean-custom-sidebar-version` (set on activation) |

### Uninstall

The plugin has no uninstall routine. Deleting it leaves the `ocean_sidebars` terms and the version option in the database. The widget areas simply stop being registered.

---

*Ocean Custom Sidebar - Unlimited custom widget areas for OceanWP*
