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

## Diagrams

Fenced ```mermaid blocks become an interactive viewer — but only when the post's
front matter has `mermaid: true`, which is what loads the renderer.

The viewer gives readers **TD / LR** buttons to switch the layout direction,
zoom in/out, **Fit** (scale to the column width, the default on load), and
fullscreen. Wide diagrams can also be dragged to pan.

The TD/LR buttons only appear when the diagram declares a direction, i.e. it
starts with `flowchart`/`graph` followed by `TB|TD|BT|LR|RL`. Other diagram
types (sequence, gantt, class, ...) still render, just without the toggle.

If a diagram's labels contain `{{ ... }}`, wrap the block in `{% raw %}` /
`{% endraw %}` so Liquid doesn't try to evaluate them.

## Writing from a browser or tablet (/admin/)

<https://geekpratyush.github.io/admin/> is a Sveltia CMS dashboard — a headless
CMS that commits Markdown straight to this repo.

**Signing in:** choose *Sign In Using Access Token* and paste a GitHub
fine-grained personal access token, scoped to this repository only, with
**Contents: read and write**. Nothing else to deploy. (The *Sign In with GitHub*
button needs a self-hosted OAuth worker — see the note in `admin/config.yml`.)

Collections mirror the section folders, plus Drafts. Saving commits to `main`,
which publishes about a minute later. Sveltia has no editorial/PR workflow yet;
to stage instead of publish, point `branch` in `admin/config.yml` at another
branch and merge when ready.

**Caution with the big technical posts.** A CMS round-trips Markdown through its
editor, which can mangle `{% raw %}` wrappers and deeply indented fenced blocks.
Use the CMS for new writing; edit posts like the Kubernetes guide in git.

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
