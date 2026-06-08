# Changelog

All notable changes to the Ready-to-Run public site are documented here.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/).

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
