# Changelog

All notable changes to the Ready-to-Run public site are documented here.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/).

## [1.3.0] - 2026-06-15

Packaged the Splash-Tours consolidated build (the draft that adds the onboarding tours).
This is the largest draft so far and is structured differently from 1.0 through 1.2, so the
packaging approach changed accordingly. Verified in a headless browser, including the
previously-dead "What We Stand For" links, which now resolve.

### Changed

- Rebuilt from the consolidated single-file draft (~13.7 MB), of which roughly 96% was
  images inlined as base64.
- Extracted 168 base64 data-URIs into 102 deduplicated binary image files under `images/`
  (~6.0 MB total), including the tour imagery. Identical payloads were collapsed to a single
  file; recognizable assets keep human-readable names, the rest use content-hash names.
- Externalized the base-app stylesheet into `css/styles.css` (~151 KB).
- Reduced `index.html` to a ~370 KB document for fast first paint.
- Regenerated the favicon set and the 1200x630 Open Graph share card.
- Updated `sitemap.xml` (`lastmod` 2026-06-15) and the structure notes in `README.md`.

### Kept inline (deliberate)

- The application script stays inline in `index.html`. This build's three onboarding splash
  tours (Marketplace, Command Center, Deployment View) are a single-file design: route-keyed
  `<template>` elements cloned at runtime by a controller wired into the hash router, with
  tour CSS hoisted on mount. Splitting the script into an external file would risk that
  verified behavior, and the script is only a small share of page weight once images are
  external. So unlike 1.0 through 1.2, there is no separate `js/` folder.

### Verified

- Headless-browser smoke test (Chromium): the home view renders on load; navigating to
  `#what-we-stand-for` activates the What We Stand For view; a gated route (`#marketplace`)
  correctly redirects to sign-in while locked and shows after unlock; all three tour
  templates are present; zero broken images; and no JavaScript errors. (The only console
  message in the offline build sandbox is the Google Fonts request, which loads normally on
  the live domain.)

### Notes

- The page `<title>` again drops the internal "(QA)" suffix
  (`Ready-to-Run · AI Campaign Staff`).
- A small URL-encoded inline SVG remains in `css/styles.css` by design (not base64).
- The on-page `<meta name="description">` is still the original draft copy; the Open Graph
  and Twitter descriptions use the product UX copy.

## [1.2.0] - 2026-06-13

Repackaged the updated application draft (13 Jun) into the deployable static site.
This draft is larger again, with more inline markup and additional artwork; the same
externalization pipeline was re-run end to end and re-verified.

### Changed

- Rebuilt from the new ~9.0 MB single-file draft (was ~7.0 MB), with more inline
  page markup and additional embedded images.
- Externalized the inline `<style>` block into `css/styles.css` (~152 KB).
- Externalized the inline `<script>` block into `js/app.js` (~158 KB), loaded
  with `defer`. Verified with `node --check`.
- Extracted 143 embedded base64 data-URIs into 99 deduplicated binary image
  files under `images/` (~5.94 MB total). Identical payloads were collapsed to
  a single file; recognizable assets keep human-readable names, the rest use
  content-hash names.
- Reduced `index.html` to a ~34 KB document (from the ~9.0 MB blocking file),
  for near-instant first paint. Total transfer is roughly 30% smaller and split
  into parallel, individually cacheable assets.
- Regenerated the favicon set and the 1200x630 Open Graph share card.
- Updated `sitemap.xml` (`lastmod` 2026-06-13) and the asset counts in
  `README.md`.

### Notes

- The page `<title>` again drops the internal "(QA)" suffix
  (`Ready-to-Run · AI Campaign Staff`).
- A small URL-encoded inline SVG remains in `css/styles.css` by design (it is
  not base64 and does not benefit from externalizing).
- The on-page `<meta name="description">` is still the original draft copy; the
  Open Graph / Twitter descriptions use the product UX copy.
- Google Fonts are still loaded from Google's CDN. See the README for a
  self-hosting option.

## [1.1.0] - 2026-06-11

Repackaged the updated application draft (06/11) into the deployable static site.
This draft is larger and adds more avatar/figure artwork; the same externalization
pipeline was re-run end to end and re-verified.

### Changed

- Rebuilt from the new ~7.0 MB single-file draft (was ~4.9 MB) with additional
  embedded artwork.
- Externalized the inline `<style>` block into `css/styles.css` (~128 KB).
- Externalized the inline `<script>` block into `js/app.js` (~155 KB), loaded
  with `defer`. Verified with `node --check`.
- Extracted 134 embedded base64 data-URIs into 91 deduplicated binary image
  files under `images/` (~4.76 MB total). Identical payloads were collapsed to
  a single file; recognizable assets keep human-readable names, the rest use
  content-hash names.
- Reduced `index.html` to a ~16 KB document (from the ~7.0 MB blocking file),
  for near-instant first paint. Total transfer is roughly 30% smaller and split
  into parallel, individually cacheable assets.
- Regenerated the favicon set and the 1200x630 Open Graph share card to match
  the current theme.
- Updated `sitemap.xml` (`lastmod` 2026-06-11) and the asset counts in
  `README.md`.

### Notes

- The page `<title>` again drops the internal "(QA)" suffix
  (`Ready-to-Run · AI Campaign Staff`).
- One small URL-encoded inline SVG remains in `css/styles.css` by design (it is
  not base64 and does not benefit from externalizing).
- The on-page `<meta name="description">` is still the original draft copy; the
  Open Graph / Twitter descriptions use the product UX copy.
- Google Fonts are still loaded from Google's CDN. See the README for a
  self-hosting option.

## [1.0.0] - 2026-06-08

First public release: the single-file application draft was unpacked into a
production-ready static site for GitHub Pages and the ready-to-run.org domain.

### Changed

- Externalized the inline `<style>` block into `css/styles.css` (125 KB),
  now cached independently of the document.
- Externalized the inline `<script>` block into `js/app.js` (115 KB), loaded
  with `defer` so it never blocks first paint. Verified with `node --check`.
- Extracted 102 embedded base64 data-URIs into 60 deduplicated binary image
  files under `images/` (~2.84 MB total). Identical payloads were collapsed to
  a single file; recognizable assets keep human-readable names (for example
  `data-analyst-asian-male.webp`, `research.webp`), the rest use content-hash
  names.
- Reduced `index.html` from a ~4.9 MB blocking download to a ~30 KB document.
  Total transfer is now roughly 37% smaller and split into parallel,
  individually cacheable assets, giving a near-instant first paint.
- Updated the page `<title>` to `Ready-to-Run · AI Campaign Staff`
  (dropped the internal "(QA)" suffix).

### Added

- `CNAME` (`ready-to-run.org`) to bind the GitHub Pages custom domain.
- `.nojekyll` so GitHub serves all files verbatim without Jekyll processing.
- `.gitignore` for OS, editor, and build cruft.
- `robots.txt` (allow all) and `sitemap.xml` pointing at the canonical home URL.
- Branded `404.html` (self-contained, dark navy theme, noindex).
- SEO and social meta in `<head>`: canonical link, `theme-color`, Open Graph
  tags, and Twitter `summary_large_image`.
- Favicon set: `favicon.svg` (root) plus `images/favicon-32.png` and
  `images/apple-touch-icon.png` (180x180).
- `images/og-image.png` (1200x630) social share card matching the site theme.
- `README.md` with the full GitHub Pages deployment guide and verified DNS
  records.

### Notes

- The on-page `<meta name="description">` was left as the original draft copy
  to avoid editorial drift. The Open Graph and Twitter descriptions use the
  product UX copy. Edit either to taste before launch.
- Google Fonts are still loaded from Google's CDN. See the README for a
  self-hosting option if you want zero third-party requests.
