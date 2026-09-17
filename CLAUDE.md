# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with
code in this repository.

## Project Overview

Quarto website project (blog listing format) on Cryptography & Software
Engineering, published to GitHub Pages at rkiy.dev.

## Common Commands

```bash
# Preview the site locally with live reload (drafts included)
quarto preview

# Render the full site to _site/ (drafts excluded)
quarto render

# Render a single post
quarto render posts/<post-name>/index.qmd
```

## Project Structure

- `_quarto.yml` — site config: `cosmo` theme, navbar, footer, `site-url`,
  `execute: freeze: auto`. Renders `*.qmd` only, so `README.md`/`CLAUDE.md`
  stay out of the site.
- `index.qmd` — homepage listing (`contents: posts`, `feed: true`, date desc).
- `about.qmd` — about page, `jolla` template.
- `posts/` — one directory per post.
  - `_metadata.yml` — shared post settings (`author`, `title-block-banner`).
  - Each post is a subdirectory with `index.qmd` plus its images.
- `styles.css` — custom CSS on top of the theme.
- `CNAME` — custom domain, copied to output via `project: resources`.
- `_site/`, `.quarto/` — generated; git-ignored, never edit.

## Creating New Posts

Create `posts/<slug>/index.qmd` with frontmatter: `title`, `date`,
`categories`, optional `image` (otherwise the first image in the post is used).
`author` is inherited from `posts/_metadata.yml`; only set it to override.
Use `draft: true` to keep a post out of `quarto render` and the RSS feed.

## Publishing

Pushing to `main` triggers `.github/workflows/publish.yml`, which renders and
pushes to the `gh-pages` branch. Do not commit rendered output.
