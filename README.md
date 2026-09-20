# kaitlynmartinhair.com

A minimal, one-page Hugo site for Kaitlyn Martin Hair — full-bleed hero photo,
booking section, deployed free via GitHub Pages + GitHub Actions.

## What's here

```
.
├── hugo.toml                  site config (name, tagline, links, Square embed)
├── content/_index.md          homepage copy
├── layouts/
│   ├── _default/baseof.html   page shell (head, css)
│   └── index.html             homepage layout (hero + booking section)
├── static/
│   ├── css/style.css          all styling
│   ├── images/hero.png        the hero photo
│   └── CNAME                  custom domain for GitHub Pages
└── .github/workflows/hugo.yaml  builds + deploys on every push to main
```

No theme submodule, no Python step — just Hugo.

## 1. Install Hugo locally (to preview before pushing)

- macOS: `brew install hugo`
- Windows: `choco install hugo-extended` or `winget install Hugo.Hugo.Extended`
- Linux: see https://gohugo.io/installation/

Then, from this folder:

```bash
hugo server -D
```

Open http://localhost:1313 to preview. `Ctrl+C` to stop.

## 2. Add the Square booking embed

In your Square Dashboard: **Online Checkout / Appointments → Share → Website
embed code**. Copy the snippet Square gives you and paste it into
`hugo.toml`, replacing the placeholder comment inside `squareEmbedCode`:

```toml
squareEmbedCode = '''
<div id="square-booking-widget"></div>
<script src="https://..."></script>
'''
```

Also fill in `instagram` and `email` in `hugo.toml` if you want those nav
links to appear (they're hidden automatically if left blank).

## 3. Push to GitHub

```bash
git init
git add .
git commit -m "Initial site"
git branch -M main
git remote add origin https://github.com/<your-username>/<repo-name>.git
git push -u origin main
```

## 4. Turn on GitHub Pages (one-time)

In the repo on GitHub: **Settings → Pages → Build and deployment → Source →
GitHub Actions**. That's it — the workflow in
`.github/workflows/hugo.yaml` will build and deploy automatically on every
push to `main`. Check the **Actions** tab for build status.

## 5. Custom domain

`static/CNAME` already contains `kaitlynmartinhair.com`, so GitHub Pages
will serve the site there once you:

1. Point your domain's DNS at GitHub Pages (an `A`/`ALIAS` record to
   GitHub's IPs, or a `CNAME` record to `<your-username>.github.io` if
   using a subdomain) — see
   https://docs.github.com/pages/configuring-a-custom-domain-for-your-github-pages-site
2. In **Settings → Pages**, enter the custom domain and enable
   "Enforce HTTPS" once it's verified.

If you'd rather use the free `<username>.github.io/<repo>` URL instead,
just delete `static/CNAME` and remove the `baseURL` line in `hugo.toml`
(the Actions workflow sets the correct base URL automatically either way).

## Editing later

- **Hero photo**: replace `static/images/hero.png` (keep the same filename,
  or update `heroImage` in `hugo.toml`).
- **Name / tagline / colors**: `hugo.toml` params, and `static/css/style.css`
  for colors (`--bg`, `--fg`, `--accent` at the top of the file).
- **Copy under the hero**: `content/_index.md`.
