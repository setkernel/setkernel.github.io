# AGENTS.md

What anyone, person or coding agent, needs to know to work in **this** repository.
`CLAUDE.md` only points here. Org-wide rules (tracking work on the board, when to stop and ask,
secrets, branches and commits, the end-of-run report) come from setkernel's central agent setup
(https://github.com/setkernel/hq/blob/main/docs/repo-standard.md); don't repeat them here.

## What this repo is
The GitHub Pages site at https://setkernel.github.io/: one static page that lets people download
the Set Kernel Root CA certificate (`SetKernel.pem`) and links back to https://setkernel.com.

## Commands
```sh
# install:  none (no package manager, no dependencies)
# dev:      python3 -m http.server 8000   # then open http://localhost:8000
# test:     none
# lint:     none
# build:    none (GitHub Pages builds it)
```
There is no CI. To check the certificate after touching it:
`openssl x509 -in SetKernel.pem -noout -subject -enddate`.

## Deploy
GitHub Pages, legacy build from the root of `master`: every push to `master` publishes the site.
There is no workflow and no secrets, so nothing in Infisical.

## Layout
- `index.html`: the whole site.
- `style.css`: the only stylesheet; sets the self-hosted Noto Sans with a `sans-serif` fallback.
- `fonts/`: the subset `woff2` with its `OFL.txt` and `PROVENANCE.txt`. Fonts follow the org rule
  (Google Fonts, self-hosted, licence beside every font file, no font CDN, no named system font).
- `SetKernel.pem`: the Set Kernel Root CA certificate (public, PEM; expires 2037-01-18).
- `.github/`: CODEOWNERS and the agent issue template.

## Traps and don't-touch
- `SetKernel.pem` is what people install as a trusted root. Don't replace or re-encode it without
  Raghav; a changed file silently changes what everyone trusts. Never commit the CA's private key.
- Everything at the root of `master` is published, including `README.md`, `AGENTS.md` and
  `CLAUDE.md`. Don't add anything that shouldn't be public.
