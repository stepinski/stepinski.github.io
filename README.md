# piotrstepinski.com

Personal site — Hugo, dark Monokai theme, deployed to GitHub Pages.

## Local dev

```bash
# Install Hugo (extended, v0.120+)
brew install hugo          # macOS
# or: https://gohugo.io/installation/

# Serve locally with live reload
hugo server -D

# Opens at http://localhost:1313
```

## Writing a new article

```bash
hugo new content articles/your-article-slug.md
```

Then edit `content/articles/your-article-slug.md`. Front matter:

```yaml
---
title: "Your Article Title"
description: "One sentence subtitle shown on list and article pages."
date: 2025-06-01
icon: "∿"          # optional decorative character (top-right of article)
draft: false
---
```

Write the article body in Markdown below the `---`.

## Deploying

Push to `main`. GitHub Actions builds and deploys automatically via the workflow in `.github/workflows/hugo.yml`.

**First-time setup:**
1. Push this repo to GitHub as `piotrstepinski.github.io` (or any repo name)
2. Go to repo **Settings → Pages**
3. Set Source to **GitHub Actions**
4. Push to `main` — done

## Customising

- **Site title, tagline, social links**: `hugo.toml`
- **Colors / fonts**: `themes/mono/static/css/main.css` (CSS variables at top)
- **Header / footer**: `themes/mono/layouts/partials/`
- **Article layout**: `themes/mono/layouts/articles/single.html`
