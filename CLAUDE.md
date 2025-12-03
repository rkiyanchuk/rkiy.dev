# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a Quarto blog focused on Cryptography & Security Engineering. It uses Quarto's website project type with a blog listing format.

## Common Commands

```bash
# Preview the site locally with live reload
quarto preview

# Render the full site to _site/
quarto render

# Render a single post
quarto render posts/<post-name>/index.qmd
```

## Project Structure

- `_quarto.yml` - Main Quarto configuration (theme: litera, navbar settings)
- `index.qmd` - Homepage with blog post listing
- `about.qmd` - About page using the "jolla" template
- `posts/` - Blog posts directory
  - `_metadata.yml` - Shared post settings (freeze: true, title-block-banner: true)
  - Each post is a subdirectory with `index.qmd` and optional images
- `_site/` - Generated output (do not edit directly)
- `styles.css` - Custom CSS overrides

## Creating New Posts

Create a new directory under `posts/` with:
- `index.qmd` with YAML frontmatter (title, author, date, categories, optional image)
- Any images or assets for the post

Posts are automatically listed on the homepage sorted by date descending.
