# rkiy.dev

Personal blog on Cryptography & Security Engineering, built with
[Quarto](https://quarto.org) and deployed to GitHub Pages at
[rkiy.dev](https://rkiy.dev).

## Prerequisites

Install Quarto (>= 1.4):

```bash
brew install --cask quarto
quarto --version
```

## Preview locally

Live-reload server at `http://localhost:4848`:

```bash
quarto preview
```

Renders the full site to `_site/` (the same output GitHub Actions builds):

```bash
quarto render
```

Render a single post (faster iteration on one piece):

```bash
quarto render posts/<post-name>/index.qmd
```

## Create a new post

1. Create a directory under `posts/` named after the post slug, e.g.
   `posts/my-new-post/`.

2. Add `index.qmd` with YAML frontmatter:

   ```yaml
   ---
   title: "My New Post"
   author: "Ruslan Kiyanchuk"
   date: "2026-05-23"
   categories: [cryptography, notes]
   image: "thumbnail.jpg"   # optional; otherwise first image in post is used
   ---
   ```

3. Drop any images/assets into the same directory and reference them with
   relative paths (e.g. `![](thumbnail.jpg)`).

4. Run `quarto preview` to see it on the homepage listing (sorted by `date`
   descending).

Shared post settings live in `posts/_metadata.yml` (currently: `freeze: true`
and `title-block-banner: true`).

## Drafts

Mark a post as a draft to keep it out of the rendered site and RSS feed:

```yaml
---
title: "Work in progress"
draft: true
---
```

`quarto preview` still renders drafts locally so you can iterate on them;
`quarto render` and the GitHub Actions publish job skip them.

## Publishing

Publishing is automatic. On every push to `main`,
[`.github/workflows/publish.yml`](.github/workflows/publish.yml) runs
`quarto render` and pushes the output to the `gh-pages` branch, which
GitHub Pages serves at the custom domain in `CNAME` (`rkiy.dev`).

Typical flow:

```bash
git add posts/my-new-post
git commit -m "Add post: my new post"
git push origin main
```

Then watch the run in the repo's **Actions** tab. The workflow can also be
triggered manually via *workflow_dispatch*.

If you ever need to publish from your laptop instead (bypassing CI), use:

```bash
quarto publish gh-pages
```

## Project structure

- `_quarto.yml` — site config (theme, navbar, footer, site URL).
- `index.qmd` — homepage with the blog listing.
- `about.qmd` — about page (jolla template).
- `posts/` — one directory per post; `_metadata.yml` holds shared post
  settings.
- `styles.css` — custom CSS overrides on top of the `cosmo` theme.
- `_site/` — rendered output (git-ignored; do not edit by hand).
- `.github/workflows/publish.yml` — CI that renders and deploys to
  `gh-pages`.
- `CNAME` — custom domain for GitHub Pages.
