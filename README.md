# Ready-to-Run · AI Campaign Staff

> Running for office shouldn't be reserved for the rich and powerful.

A marketplace and operations interface for **AI campaign staff** · explore departments,
assemble a team of specialized agents, and run them from a campaign command center.

**Live site:** https://ready-to-run.org

This repository is a **static site** (no build step, no server). The browser loads
`index.html`, which pulls in the stylesheet and the image assets. The application
script is kept inline in `index.html` (see the note under "Good to know"), so there
is no separate `js/` folder. Everything is plain HTML/CSS/JS and deploys directly to
GitHub Pages.

---

## What's in this repo

```
.
├── index.html              # entry point (inline app script; loads css + images)
├── css/
│   └── styles.css          # base site styles
├── images/                 # 102 binary image assets (avatars, figures, art, tour imagery)
│   ├── og-image.png        # 1200×630 social-share card
│   ├── favicon-32.png
│   └── apple-touch-icon.png
├── favicon.svg             # vector favicon (preferred by modern browsers)
├── CNAME                   # custom domain (ready-to-run.org)
├── 404.html                # branded not-found page
├── robots.txt              # crawler directives + sitemap pointer
├── sitemap.xml             # single-page sitemap
├── .nojekyll               # tells GitHub Pages to skip Jekyll processing
├── .gitignore
├── README.md
└── CHANGELOG.md
```

---

## Deploy to GitHub Pages

### 1. Create the repository and push these files

The repo can have **any** name (the custom domain is what matters), and it must be
**public** for free GitHub Pages.

```bash
# from inside this folder
git init
git add .
git commit -m "Initial deploy: Ready-to-Run static site"
git branch -M main
git remote add origin https://github.com/<your-username>/<repo-name>.git
git push -u origin main
```

### 2. Turn on GitHub Pages

In the repo on GitHub: **Settings → Pages**

- **Source:** *Deploy from a branch*
- **Branch:** `main`  ·  **Folder:** `/ (root)`
- Click **Save**

GitHub builds the site and gives you a temporary `https://<your-username>.github.io/<repo-name>/` URL.

### 3. Custom domain

The included `CNAME` file already sets the domain to `ready-to-run.org`, so once you push,
GitHub Pages picks it up automatically. Confirm it under **Settings → Pages → Custom domain**
(it should read `ready-to-run.org`). GitHub will run a DNS check next.

### 4. Point DNS at GitHub (at your domain registrar)

Create these records for **ready-to-run.org**. Values are GitHub's official Pages addresses:

**Apex domain · A records** (host `@`)

```
185.199.108.153
185.199.109.153
185.199.110.153
185.199.111.153
```

**Apex domain · AAAA records (IPv6, recommended)** (host `@`)

```
2606:50c0:8000::153
2606:50c0:8001::153
2606:50c0:8002::153
2606:50c0:8003::153
```

**www subdomain · CNAME record**

```
Host:  www
Value: <your-username>.github.io
```

**(Recommended) Verify your domain** to prevent takeovers: GitHub → your
**Profile → Settings → Pages → Add a domain**, then add the `TXT` record it gives you.

> DNS changes can take anywhere from a few minutes to 24 hours to propagate.
> Check with: `dig ready-to-run.org +noall +answer -t A`

### 5. Enforce HTTPS

Once the DNS check passes, return to **Settings → Pages** and tick **Enforce HTTPS**.
GitHub provisions a free TLS certificate automatically (this can take up to ~24h after
DNS resolves).

### Updating the site later

```bash
git add .
git commit -m "Update site"
git push
```

GitHub Pages redeploys on every push to `main`.

---

## Preview locally

External assets need to be served over HTTP (not opened as a `file://` path), so run a
tiny local server from this folder:

```bash
python3 -m http.server 8000
# then open http://localhost:8000
```

---

## Build notes

- **Images and the base stylesheet are externalized for performance.** The source draft
  was a single ~13.7 MB HTML file, ~96% of which was images inlined as base64. Those are
  now 102 deduplicated binary files under `images/` (browser-cacheable, loaded in
  parallel), and the base stylesheet lives in `css/styles.css`. The HTML document itself
  is now ~370 KB, so first paint is fast.
- **The application script is intentionally inline.** This build includes the onboarding
  splash tours, which are a single-file design: route-keyed `<template>` elements cloned
  at runtime by a controller wired into the hash router. Splitting the script into an
  external file would risk that verified behavior for little benefit (the script is a
  small share of the page weight once images are externalized), so it stays in
  `index.html`. See `CHANGELOG.md` for details.
- **Fonts** (Sora, Inter, Geist Mono) load from Google Fonts via the `<link>` tags in
  `index.html`. If you'd prefer to self-host them (slightly faster, avoids a third-party
  request), download the font files into `css/fonts/` and add `@font-face` rules.
- **Routing** uses URL hashes (`#what-we-stand-for`, `#marketplace`, `#command-center`,
  `#deployment-view`), which work out of the box on GitHub Pages · no SPA redirect tricks
  needed.
- **Two production tweaks** were applied when packaging: the `<title>` lost its `(QA)`
  label, and full Open Graph / Twitter / favicon metadata was added. If you want the
  on-page `<meta name="description">` reworded for SEO too, edit it in `index.html` · it
  still carries the original draft copy.
