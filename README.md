# 0xctnc.github.io

Personal cybersecurity portfolio for 0xctnc. GitHub Pages serves it at https://0xctnc.github.io.

## Layout

- `index.html` — homepage
- `404.html` — response for unknown paths
- `favicon.svg` — site icon
- `assets/` — static files. The stylesheet is `assets/css/site.css`
- `_config.yml` — Jekyll config for GitHub Pages. It excludes `.github/`, `.yamllint.yml`, `README.md`, and `SECURITY.md` from the published site
- `SECURITY.md` — how to report a vulnerability
- `.gitignore` — ignores secret files, editor files, and local Jekyll output (`_site/`, `.jekyll-cache/`, `.sass-cache/`)
- `.yamllint.yml` — yamllint rules for CI
- `.github/workflows/validate.yml` — yamllint and gitleaks on pull requests and on pushes to `main`
- `.github/workflows/main-pr-check.yml` — checks that commits pushed to `main` come from a pull request merged into `main`
- `.github/dependabot.yml` — weekly update pull requests for GitHub Actions
- `.github/CODEOWNERS` — code owners for the repository

## Build and deploy

The pages are static HTML and CSS. GitHub Pages publishes the `main` branch from the repository root with its built-in Jekyll build, and HTTPS is enforced. `_config.yml` lists the paths Jekyll leaves out of the published site. No GitHub Actions workflow builds or deploys the site.

## Local preview

From the repository root:

```sh
python3 -m http.server
```

Open the local URL the server prints. That serves `index.html` and the stylesheet as static files. It does not run Jekyll.

## Security

`index.html` and `404.html` set this Content-Security-Policy:

`default-src 'none'; style-src 'self'; img-src 'self'; base-uri 'none'; form-action 'none'`

The pages load no third-party scripts. Styling comes from `assets/css/site.css` on this site, and the CSS uses system fonts.

On each pull request, and on each push to `main`, `.github/workflows/validate.yml` runs yamllint and scans git history with gitleaks.

## Changes

Update the site through a pull request into `main`. After a push to `main`, `.github/workflows/main-pr-check.yml` checks that every new commit is associated with a pull request merged into `main`.
