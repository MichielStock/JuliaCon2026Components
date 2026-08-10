# JuliaCon2026Components

## Getting Started
- Use Dyad Agent to create your own component
- Play around with its physics.
- Generate cool visualisations that you would like to submit to our gallery.
- Add your final visualisation as a page at `viz_submission/index.html`.
- Open a PR to this repo with title: `<What you built in a single sentence>`. Eg. 'Two Stroke Engine'.
- Write a short description in the PR body — the gallery shows it when someone hovers over your card.

## How the gallery works

Every PR is published to the live gallery automatically. Your card shows your
GitHub username, your PR title, and (on hover) your PR description; clicking
it opens your submission full size. Pushing new commits or editing the PR
title/description republishes your card.

Your `index.html` must be a single self-contained file (max 1.5 MB): inline
your CSS/JS. Relative asset paths won't work — reference images either as
`data:` URIs or by commit-pinned GitHub raw URL, e.g.
`https://raw.githubusercontent.com/<user>/<repo>/<commit-sha>/viz_submission/foo.png`.

## For organisers

`.github/workflows/publish-to-gallery.yml` publishes submissions. It needs two
repo secrets (Settings → Secrets and variables → Actions):

- `GALLERY_API_URL` — the gallery server, no trailing slash
  (e.g. `https://scoreboard-production-df34.up.railway.app`)
- `GALLERY_CI_KEY` — the key configured as `CI_KEY` on the gallery server

The workflow uses `pull_request_target` so fork PRs can publish too; it never
executes participant code — it only reads files from `viz_submission/` and
uploads them.
