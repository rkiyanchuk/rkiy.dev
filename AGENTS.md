# Repository Guidelines

Quarto website project (blog listing format) on Cryptography & Software
Engineering, published to GitHub Pages at [rkiy.dev](https://rkiy.dev). No
tests, no build step beyond `quarto render`.

## Commands

```bash
quarto preview                          # live reload, drafts included
quarto render                            # full site to _site/, drafts excluded
quarto render posts/<slug>/index.qmd     # single post
quarto check                             # verify toolchain
```

## Layout

- `_quarto.yml` — site config: `theme: [litera, custom.scss]`, navbar, footer,
  `site-url`, `execute: freeze: auto`. Renders `*.qmd` only, so
  `README.md`/`AGENTS.md` stay out of the site.
- `custom.scss` — SCSS layer over `litera`; `fonts/` — self-hosted woff2.
- `index.qmd` — homepage listing (`contents: posts`, `feed: true`, date desc).
- `about.qmd` — about page, `jolla` template.
- `posts/<slug>/index.qmd` — one directory per post, images alongside it.
  `posts/_metadata.yml` holds shared settings (`author`).
- `CNAME` — custom domain, copied to output via `project: resources`. Required
  for the custom domain; `gh-pages` serves it.
- `_site/`, `.quarto/` — generated; git-ignored, never edit or commit.

## Conventions

- Post frontmatter: `title`, `date`, `categories`, optional `image` (otherwise
  the first image in the post is used). `author` is inherited from
  `posts/_metadata.yml` — set it only to override.
- `draft: true` keeps a post out of `quarto render` and the RSS feed;
  `quarto preview` still shows it.
- Styling lives in `custom.scss` as an SCSS layer over `litera` — never a plain
  CSS file. It currently only sets fonts: IBM Plex Serif for prose/headings,
  Iosevka Nerd Font for code, self-hosted from `fonts/` (see
  `fonts/README.md`). `url()` paths there are project-relative; Quarto copies
  the faces to `site_libs/bootstrap/fonts/`. No third-party font CDNs.
- Prose in Markdown wraps at 80 columns.

## Publishing

Pushing to `main` triggers `.github/workflows/publish.yml`, which renders and
pushes to the `gh-pages` branch. Never commit rendered output.
