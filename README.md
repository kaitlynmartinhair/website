# kaitlynmartinhair.com

A minimal, one-page Hugo site for Kaitlyn Martin Hair — full-bleed hero photo,
"Book Now" links out to Square Appointments, deployed free via GitHub Pages +
GitHub Actions.

## What's here

```
.
├── hugo.toml                  site config (name, tagline, links, booking URL)
├── content/_index.md          homepage copy
├── layouts/
│   ├── _default/baseof.html   page shell (head, nav, footer)
│   └── index.html             homepage layout (hero, intro, location)
├── static/
│   ├── css/style.css          all styling
│   ├── images/hero.png        the hero photo
│   └── CNAME                  custom domain for GitHub Pages
└── .github/workflows/hugo.yaml  builds + deploys on every push to master
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

## 2. Point "Book Now" at Square Appointments

Every "Book Now" button opens `bookingUrl` from `hugo.toml` directly in a
new tab — no embed needed:

```toml
bookingUrl = "https://book.squareup.com/appointments/..."
```

Also fill in `email` in `hugo.toml` if you want the "Contact" nav link to
appear (it's hidden automatically if left blank).

## 3. Push to GitHub

```bash
git init
git add .
git commit -m "Initial site"
git branch -M master
git remote add origin https://github.com/<your-username>/<repo-name>.git
git push -u origin master
```

## 4. Turn on GitHub Pages (one-time)

In the repo on GitHub: **Settings → Pages → Build and deployment → Source →
GitHub Actions**. That's it — the workflow in
`.github/workflows/hugo.yaml` will build and deploy automatically on every
push to `master`. Check the **Actions** tab for build status.

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
