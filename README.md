# geekpratyush.github.io

My personal site and blog — Jekyll on GitHub Pages, live at <https://geekpratyush.github.io>.

GitHub builds the site automatically on every push to `main`. Nothing to install, no
workflow to run.

## Adding a post

Create a Markdown file in the folder for its section — the folder name *is* the section,
so no `categories:` line is needed:

```
_posts/it-design/YYYY-MM-DD-some-slug.md
_posts/coding/YYYY-MM-DD-some-slug.md
_posts/devops/YYYY-MM-DD-some-slug.md
_posts/life/YYYY-MM-DD-some-slug.md
```

Front matter:

```markdown
---
title: "Your title here"
description: "One or two sentences — shown in post lists and search results."
tags: [java, kubernetes]
mermaid: true      # only if the post contains a ```mermaid diagram
---

Your post, in Markdown.
```

The date in the filename is the publish date. Commit, push, wait about a minute.

The blog index, the section pages, the homepage cards and the post counts all update
themselves — there are no lists to hand-edit.

**Drafts:** put the file in a `_drafts/` folder with no date in the filename; it won't
publish. Preview with `bundle exec jekyll serve --drafts`.

## Adding a new section

1. Add an entry to `_data/sections.yml` (`slug`, `title`, `icon`, `blurb`).
2. Copy an existing file in `topics/` to `topics/<slug>.md`, setting `section:` and
   `permalink:` to the new slug.
3. Start putting posts in `_posts/<slug>/`.

## Pages

| File | URL |
|---|---|
| `index.html` | `/` — profile, about, skills, featured work, writing |
| `projects.html` | `/projects.html` |
| `blog.html` | `/blog.html` — all posts, grouped by year |
| `topics/<slug>.md` | `/<slug>/` — one landing page per section |
| `_posts/<slug>/…` | `/<slug>/<post-title>/` |

## Layout

```
_config.yml          site settings
_data/sections.yml   the list of blog sections
_layouts/            default, post, section
_includes/           nav, section-nav, post-list, mermaid
_posts/<section>/    posts, one folder per section
topics/              one landing page per section
style.css            all styling
```

## Running it locally (optional)

Only needed if you want a preview before pushing:

```bash
bundle install
bundle exec jekyll serve   # http://localhost:4000
```
