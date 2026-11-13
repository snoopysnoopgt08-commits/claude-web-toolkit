---
name: core-web-vitals-auditor
description: Audit and fix theme/site code for Core Web Vitals (LCP, CLS, INP) — enforce image lazy-loading, font-display swap, and deferring non-critical JS. Use when reviewing performance of Shopify, WordPress, or static site templates, or when asked to optimize page speed.
---

# Core Web Vitals Auditor

Review templates, CSS and JS and report/fix issues hurting LCP, CLS and INP.

## Checklist (enforce all)

### Images (LCP, CLS)
- Below-the-fold images: `loading="lazy"` and `decoding="async"`.
- The LCP/hero image: **not** lazy — `loading="eager"` + `fetchpriority="high"`, and optionally `<link rel="preload" as="image">`.
- Every `<img>`/`<video>`/`<iframe>` has explicit `width` and `height` (or CSS `aspect-ratio`) to prevent layout shift.
- Responsive `srcset` + `sizes`; modern formats (WebP/AVIF) where the platform supports it.

### Fonts (LCP, CLS)
- Every `@font-face` has `font-display: swap` (or `optional`).
- Preload only the 1–2 critical font files with `<link rel="preload" as="font" type="font/woff2" crossorigin>`.
- `preconnect` to third-party font origins; prefer self-hosted WOFF2.

### JavaScript (INP, LCP)
- Non-critical scripts use `defer` (or `type="module"`); third-party widgets load `async` or on interaction/idle.
- No render-blocking JS in `<head>`.
- Break up long tasks; avoid heavy work in input handlers; use passive listeners for scroll/touch.
- Remove unused libraries (e.g. jQuery if not needed).

### CSS
- Inline critical above-the-fold CSS; load the rest without blocking where possible.
- Reserve space for dynamic content (banners, embeds, ads) to avoid CLS.
- Avoid animating layout properties; animate `transform`/`opacity`.

## Output format

For each finding: file:line, metric affected (LCP/CLS/INP), severity, and the exact fix. Then apply fixes when asked.
