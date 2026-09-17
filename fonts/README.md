# Self-hosted webfonts

- **IBM Plex Serif** — prose and headings. SIL Open Font License 1.1,
  <https://github.com/IBM/plex>.
- **Iosevka Nerd Font** — code. SIL Open Font License 1.1,
  <https://github.com/be5invis/Iosevka> (patched by
  <https://github.com/ryanoasis/nerd-fonts>).

Both are OFL, so redistribution inside this repository is permitted.

Faces are latin + latin-ext + Greek + arrows/math subsets of the TTFs in
`~/Library/Fonts`, converted to `woff2`. Nerd Font icon planes are dropped:
they are unused in prose and cost megabytes.

Regenerate after a font upgrade:

```bash
SRC="$HOME/Library/Fonts"
RANGE="U+0000-00FF,U+0131,U+0152-0153,U+02BB-02BC,U+02C6,U+02DA,U+02DC,\
U+0304,U+0308,U+0329,U+2000-206F,U+2074,U+20AC,U+2122,U+2191,U+2193,\
U+2212,U+2215,U+FEFF,U+FFFD,U+0100-017F,U+0180-024F,U+0370-03FF,\
U+2190-21FF,U+2200-22FF,U+2264-2265"

for f in IBMPlexSerif-Regular IBMPlexSerif-Italic IBMPlexSerif-Bold \
         IBMPlexSerif-BoldItalic IosevkaNerdFont-Regular \
         IosevkaNerdFont-Italic IosevkaNerdFont-Bold; do
  uvx --from "fonttools[woff]" pyftsubset "$SRC/$f.ttf" \
    --unicodes="$RANGE" --layout-features='*' --flavor=woff2 \
    --output-file="fonts/$(echo "$f" | tr 'A-Z' 'a-z').woff2"
done
```

`@font-face` declarations live in `custom.scss`.
