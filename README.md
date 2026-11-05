# Eli M. Nate — author site

Static site for the Eli M. Nate murder-mystery elimination puzzle book series.
Deploys automatically to GitHub Pages on every push to `main`.

## One-time setup (do this once)

### 1. Buy the domain
Buy your chosen domain through Hostinger (or wherever). This repo currently
assumes **eliminationmysteries.com** — if you land on a different one, edit
the `CNAME` file in this repo (just the one line, the domain name) to match.

### 2. Turn on GitHub Pages for this repo
In this repo on GitHub: **Settings → Pages**
- Under "Build and deployment," **Source** should be **GitHub Actions**
  (the workflow in `.github/workflows/pages.yml` handles the rest).
- Under "Custom domain," enter your domain (e.g. `eliminationmysteries.com`)
  and save. GitHub will show a DNS check — it will fail until step 3 is done.
- Once DNS is correct (can take a few minutes to a few hours), come back and
  check **Enforce HTTPS**.

### 3. Point the domain at GitHub, in Hostinger's DNS panel
Hostinger: **Domains → [your domain] → DNS / Nameservers → DNS Zone Editor**

Add these records (delete any existing A/CNAME records on the same names
first, e.g. Hostinger's default parking page records):

| Type  | Name / Host | Value                  |
|-------|-------------|------------------------|
| A     | @           | 185.199.108.153        |
| A     | @           | 185.199.109.153        |
| A     | @           | 185.199.110.153        |
| A     | @           | 185.199.111.153        |
| CNAME | www         | 1-wpp.github.io         |

("@" means the bare domain, e.g. `eliminationmysteries.com` with nothing in
front of it. Hostinger may call this "root" or leave the Name field empty.)

DNS changes can take anywhere from a few minutes to ~24 hours to take effect
everywhere. Once it has, both `eliminationmysteries.com` and
`www.eliminationmysteries.com` will load the site, and GitHub will issue a
free HTTPS certificate automatically.

## Making changes later

Ask Claude (in a session with this repo attached) for the change you want.
Claude edits `index.html` (and files in `img/` for new covers or art),
commits, and pushes to `main`. The GitHub Action picks it up automatically —
**no manual upload, no dragging folders.** The live site updates within
about a minute of the push.

To add a new book: add its cover image to `img/`, then add a new `<article
class="case ...">` block to `index.html` following the pattern of the
existing three, and update the counts in the pink stats bar.

## Structure

```
index.html   — the whole site (single page, all CSS/JS inline except fonts)
img/         — book covers + logo
CNAME        — your custom domain, read by GitHub Pages
.github/workflows/pages.yml — auto-deploy on push to main
```
