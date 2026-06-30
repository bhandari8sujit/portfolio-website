# Sujit Bhandari — Portfolio

A fast, responsive, single-page developer portfolio built with vanilla HTML, CSS, and
JavaScript (no build step). Features a dark/light theme, scroll-reveal animations,
a terminal-style hero, a dedicated **Publications & Patents** section, and a fully
responsive layout.

## Project structure

```
portfolio-webst/
├── index.html              # Page markup / all content
├── styles.css              # Styles + theming + dev-themed UI + responsive rules
├── script.js               # Nav, theme toggle, scroll reveal
├── resume.pdf              # Downloadable résumé (linked from nav + hero + contact)
├── CNAME                   # Custom domain for GitHub Pages
├── .nojekyll               # Disables Jekyll processing on Pages
└── .github/workflows/
    └── deploy.yml          # GitHub Actions deploy workflow
```

> **Add your résumé:** drop your latest PDF in the repo root named `resume.pdf`.
> The **Resume** button in the nav, the **Download résumé** button in the hero, and
> the contact links all point to `resume.pdf`.

## Run locally

It's a static site — just open `index.html` in a browser, or serve it:

```powershell
# Option 1: Python
python -m http.server 5500

# Option 2: VS Code "Live Server" extension → "Go Live"
```

Then visit http://localhost:5500.

---

## Deploy to GitHub Pages with GitHub Actions + a custom domain

### 1. Create the GitHub repository

```powershell
cd c:\Users\SujitBhandari\portfolio-webst
git init
git add .
git commit -m "Initial portfolio site"
git branch -M main
```

Create an empty repo on GitHub (e.g. `portfolio`), then:

```powershell
git remote add origin https://github.com/<your-username>/<repo-name>.git
git push -u origin main
```

### 2. Enable GitHub Pages with the Actions source

1. On GitHub, open the repo → **Settings** → **Pages**.
2. Under **Build and deployment** → **Source**, select **GitHub Actions**.

The workflow in `.github/workflows/deploy.yml` runs on every push to `main`,
uploads the site, and deploys it. Watch progress in the **Actions** tab.

### 3. Point your custom domain to GitHub Pages (DNS)

At your domain registrar (Namecheap, GoDaddy, Cloudflare, etc.), add records.

**For a subdomain (recommended, e.g. `www.yourdomain.com`):**

| Type  | Host / Name | Value                       |
| ----- | ----------- | --------------------------- |
| CNAME | `www`       | `<your-username>.github.io` |

**For the apex / root domain (e.g. `yourdomain.com`)** add four A records and
the AAAA records for IPv6:

| Type | Host | Value           |
| ---- | ---- | --------------- |
| A    | `@`  | `185.199.108.153` |
| A    | `@`  | `185.199.109.153` |
| A    | `@`  | `185.199.110.153` |
| A    | `@`  | `185.199.111.153` |
| AAAA | `@`  | `2606:50c0:8000::153` |
| AAAA | `@`  | `2606:50c0:8001::153` |
| AAAA | `@`  | `2606:50c0:8002::153` |
| AAAA | `@`  | `2606:50c0:8003::153` |

> Tip: To use both the apex and `www`, add the A/AAAA records for `@` **and** a
> CNAME for `www`. GitHub will redirect one to the other automatically.

### 4. Set the custom domain in the repo

1. Edit the `CNAME` file in this repo and replace `www.yourdomain.com` with your
   actual domain (e.g. `www.sujitbhandari.dev` or `sujitbhandari.dev`). Commit and push.
   - The `CNAME` file must contain **only** the domain, one line, no `https://`.
2. Alternatively (or additionally), go to **Settings → Pages → Custom domain**,
   enter your domain, and click **Save**. GitHub writes/updates the `CNAME` file.

### 5. Wait for DNS + enable HTTPS

1. DNS propagation can take from a few minutes up to ~24 hours.
2. In **Settings → Pages**, GitHub will show a green **DNS check successful**.
3. Tick **Enforce HTTPS** once the certificate is provisioned (this can take an
   extra hour after the DNS check passes).

Your site is now live at your custom domain. Every push to `main` redeploys it.

---

## Updating the site

Edit `index.html`, `styles.css`, or `script.js`, then:

```powershell
git add .
git commit -m "Update content"
git push
```

The Actions workflow redeploys automatically.

## Troubleshooting

- **404 after first deploy:** Make sure **Settings → Pages → Source** is set to
  **GitHub Actions** (not "Deploy from a branch").
- **Custom domain keeps clearing:** The `CNAME` file must exist in the deployed
  site. It's included here, so keep it in the repo root.
- **HTTPS option greyed out:** Wait for the DNS check to pass first, then retry.
- **Styles missing:** The `.nojekyll` file prevents Jekyll from ignoring files;
  keep it in the repo root.
