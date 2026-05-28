# Personal website

Built with [Quarto](https://quarto.org). Deployed to GitHub Pages via GitHub Actions.

## One-time setup

1. **Install Quarto** locally so you can preview before pushing:
   ```bash
   # macOS
   brew install --cask quarto
   ```
   Verify: `quarto --version`.

2. **Replace placeholders.** Search and replace these across the repo:
   - `SamarthSheth` → your GitHub handle
   - `samarthsheth.github.io` → this repo's name
   - `samarth-sheth` → your LinkedIn slug
   - `samarth.sheth@hotmail.com` → your email
   - Update `site-url` in `_quarto.yml`

   On macOS:
   ```bash
   grep -rl 'SamarthSheth' . | xargs sed -i '' 's/SamarthSheth/samarth/g'
   ```

3. **Add a profile image.** Drop `profile.jpg` in the repo root (any square image works — the homepage uses it).

4. **(Optional) Add your CV PDF.** Put `cv.pdf` in the repo root.

5. **Enable GitHub Pages.** In repo Settings → Pages → set Source to "Deploy from a branch", Branch: `gh-pages` / root. The first deploy creates that branch automatically.

## Daily workflow

### Preview locally
```bash
quarto preview
```
Opens `http://localhost:nnnn` with hot reload.

### Add a project
Create `projects/my-project.qmd`. Use `projects/nebula.qmd` as a template — copy the front matter and edit. It auto-appears on the projects listing page.

### Add a blog post
Create `blog/posts/my-post.qmd`. Front matter needs at minimum:
```yaml
---
title: "Post title"
date: "2026-05-27"
categories: [topic]
description: "One-line summary."
---
```

### Math
Inline: `$E = mc^2$`. Display:
```
$$
\int_0^\infty e^{-x^2}\, dx = \frac{\sqrt{\pi}}{2}
$$
```
Rendered with KaTeX (configured in `_quarto.yml`).

### Code
Fenced blocks with a language tag get syntax highlighting:
````
```python
def f(x): return x + 1
```
````

### Deploy
```bash
git add .
git commit -m "update"
git push
```
GitHub Actions builds and publishes to the `gh-pages` branch automatically. Live in ~1–2 minutes.

## Structure

```
.
├── _quarto.yml              # site config — nav, theme, math
├── index.qmd                # homepage
├── about.qmd
├── cv.qmd
├── styles.css               # custom CSS
├── projects/
│   ├── index.qmd            # auto-listing
│   └── *.qmd                # one file per project
├── blog/
│   ├── index.qmd            # auto-listing
│   └── posts/*.qmd          # one file per post
└── .github/workflows/publish.yml
```

## Adding more top-level pages

E.g. a "Teaching" page:
1. Create `teaching.qmd`.
2. Add to `_quarto.yml` navbar:
   ```yaml
   navbar:
     left:
       - href: teaching.qmd
         text: Teaching
   ```

## Themes

Currently using `cosmo` (light) / `darkly` (dark). To change, edit `_quarto.yml` → `format.html.theme`. Full list: <https://quarto.org/docs/output-formats/html-themes.html>.
