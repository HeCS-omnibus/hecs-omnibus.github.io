# hecs-omnibus.github.io

Webpage for **HeCS-omnibus** — the Hectospec Cluster Survey omnibus catalog
(Sohn et al. 2020, ApJ 891, 129).

## Layout

| Path | Purpose |
|---|---|
| `webpage/` | The site itself. Published to https://hecs-omnibus.github.io/ |
| `reference/` | Local literature cache (PDFs + arXiv LaTeX sources). **Not tracked** — see `.gitignore` |
| `.github/workflows/pages.yml` | Deploys `webpage/` to GitHub Pages on push to `main` |

## Deployment

The Pages source must be set to **GitHub Actions**
(Settings → Pages → Build and deployment → Source: GitHub Actions).
