# blog

Source for my personal blog, **Notes & Posts** — built with [Hugo](https://gohugo.io/) and the [hugo-book](https://github.com/alex-shpak/hugo-book) theme.

Published via GitHub Pages: https://mobiledge.github.io/blog/

## Structure

```
content/
  _index.md            # landing page
  posts/
    _index.md          # blog section
    <post>.md          # one Markdown file per post
```

Posts use hugo-book's blog layout (`BookSection = "posts"`): they're listed newest-first by `date`. Each post has a broad `category` (Coding or Life) and finer-grained `tags` (Swift, SwiftUI, Tooling, ...), surfaced as taxonomy pages under `/categories/` and `/tags/`.

## Local development

```bash
git clone --recurse-submodules https://github.com/mobiledge/blog.git
cd blog
hugo server
```

If you already cloned without `--recurse-submodules`:

```bash
git submodule update --init --recursive
```

## Adding a post

Create a Markdown file under `content/posts/` with front matter:

```yaml
---
title: "Your Post Title"
date: 2026-01-15
categories: ["Coding"]   # Coding or Life
tags: ["Swift"]          # optional: Swift, SwiftUI, Tooling, ...
---
```

## Deployment

Pushing to `main` triggers the GitHub Actions workflow in `.github/workflows/hugo.yml`, which builds the site and deploys it to GitHub Pages.

---

_Disclaimer: If my words sound smarter than I actually am, that's because I often get AI help when putting my thoughts into words. (this disclaimer included)_
