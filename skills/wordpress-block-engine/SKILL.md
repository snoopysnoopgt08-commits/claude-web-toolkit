---
name: wordpress-block-engine
description: Build WordPress Gutenberg blocks and ACF field groups — block.json structures, dynamic PHP render templates, ACF blocks, theme.json settings. Use when creating or editing WordPress block themes, custom blocks, or Advanced Custom Fields configurations.
---

# WordPress Block Engine

Define Gutenberg block structures and ACF fields.

## Rules

- Every block is registered from a **`block.json`** (apiVersion 3) with `name` (`namespace/block-name`), `title`, `category`, `icon`, `description`, `supports`, `attributes`, `textdomain`, and `editorScript` / `style` / `viewScript` / `render` as needed.
- Register with `register_block_type( __DIR__ . '/build/block-name' )` on `init`.
- Prefer **dynamic blocks** (`render.php`) for content pulled from the DB; static `save()` only for pure markup.
- Use `get_block_wrapper_attributes()` on the root element in `render.php`.
- **ACF blocks**: `block.json` with `"acf": { "mode": "preview", "renderTemplate": "render.php" }`; fields via `get_field()`. Export ACF field groups as PHP (`acf_add_local_field_group`) or `acf-json/` so they're version-controlled. Every field has a unique `key` (`field_...`).
- Escape all output: `esc_html()`, `esc_attr()`, `esc_url()`, `wp_kses_post()`. Sanitize input. Use nonces for forms.
- All strings translatable: `__()`, `_e()`, `esc_html__()` with the theme/plugin textdomain.
- Global styles/settings go in `theme.json` (colors, typography, spacing presets) rather than hard-coded CSS.
- Frontend interactivity: vanilla JS `viewScript` (or the Interactivity API). No React on the frontend unless explicitly requested; React is only for the editor side (`edit.js`).
- Enqueue assets conditionally — only on pages where the block is present.

## Layout

```
blocks/block-name/
  block.json
  edit.js
  render.php
  style.css
  editor.css
  view.js
```
