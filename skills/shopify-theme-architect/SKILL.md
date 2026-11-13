---
name: shopify-theme-architect
description: Generate clean Shopify Online Store 2.0 theme code — sections, blocks, snippets, and {% schema %} JSON settings in native Liquid, vanilla CSS and vanilla JS. Use when building or editing .liquid files, section schemas, theme blocks, or templates/*.json in a Shopify theme.
---

# Shopify Theme Architect

Generate clean Shopify sections, blocks, and schema JSON settings.

## Rules

- **Always include `{% schema %}` settings** so merchants can customize the section in the Shopify Theme Editor (text, image_picker, color, range, select, checkbox, url, richtext, etc.).
- Every section schema includes: `name`, `tag`, `class`, `settings`, relevant `blocks` (with `@app` block where appropriate), and `presets` so it can be added from the editor.
- Schema is strict JSON: no comments, no trailing commas, unique `id`s, valid setting `type`s only.
- Use `{{ block.shopify_attributes }}` on every block wrapper and loop blocks with `{% for block in section.blocks %}` + `{% case block.type %}`.
- Native Liquid only — never React/JSX. Vanilla CSS (scoped with `#shopify-section-{{ section.id }}` or a section class) and vanilla JS (Web Components / `customElements.define`, `defer`).
- Prefer `{% render %}` over `{% include %}`. Pass variables explicitly.
- Images: `{{ image | image_url: width: 1500 | image_tag: loading: 'lazy', widths: '375, 750, 1100, 1500', sizes: '(min-width: 750px) 50vw, 100vw' }}`. Use `loading: 'eager'` + `fetchpriority: 'high'` only for the above-the-fold hero.
- Translatable strings go in `locales/*.json` and use `{{ 'key' | t }}`; schema labels can use `t:` keys.
- Only use documented Liquid objects, tags and filters. If unsure a filter exists, say so instead of inventing it.
- Load section CSS with `{{ 'section-name.css' | asset_url | stylesheet_tag }}` and JS with `<script src="{{ 'section-name.js' | asset_url }}" defer></script>`.

## File layout

```
sections/   — section .liquid files with {% schema %}
blocks/     — theme blocks (OS 2.0 theme blocks)
snippets/   — reusable partials ({% render %})
assets/     — CSS/JS/images
templates/  — JSON templates
config/     — settings_schema.json, settings_data.json
locales/    — translations
```
