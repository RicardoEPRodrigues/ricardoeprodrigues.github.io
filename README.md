# colorcrow.me

Personal website and blog of Ricardo "Colorcrow" Rodrigues, live at **[colorcrow.me](https://colorcrow.me)**.

It's a [Jekyll](https://jekyllrb.com/) site hosted on GitHub Pages originally built on the [Indigo](https://github.com/sergiokopplin/indigo) theme and now restyled as "Verdigris Codex", a medieval-illumination design kept in `pencil/design.pen`.

## Quick start

You need Ruby **2.7.x** and Bundler. The `github-pages` gem pins Jekyll 3.9, which runs most reliably on Ruby 2.7. The repo ships a `.ruby-version` file, so `rbenv` or `asdf` pick up the right version automatically.

```bash
# 1. Install the pinned Ruby (rbenv example)
rbenv install 2.7.6

# 2. Install gems
gem install bundler
bundle install

# 3. Run the dev server with live reload
bundle exec jekyll serve --livereload --drafts
```

Then open <http://localhost:4000>.

`--drafts` also renders the files in `_drafts/`. Leave it off to see exactly what will be published.

### Other commands

| Command | What it does |
| --- | --- |
| `bundle exec jekyll build` | Builds the site into `_site/` |
| `bundle exec rake` | Runs `html-proofer` on `_site/` to find broken links and images (build first) |
| `bundle exec rake cv` | Copies the latest CV into the site (see [Updating the résumé](#updating-the-résumé)) |
| `bundle update github-pages` | Updates to the Jekyll and plugin versions that GitHub Pages currently runs |

### Troubleshooting

- **`nokogiri`, `eventmachine` or `ffi` fail to compile.** Install your system's build tools and dev headers. On Debian or Ubuntu that's `sudo apt install build-essential ruby-dev zlib1g-dev`.
- **`cannot load such file -- webrick`.** You're on Ruby 3.x. Either switch to 2.7, or check that `webrick` is still in the `Gemfile`.
- **Your changes don't show up.** `_config.yml` isn't watched by the dev server, so restart `jekyll serve` after editing it.

## Project layout

```
_config.yml        Site settings: title, bio, colours, social links, feature toggles
_posts/            Blog posts, named YYYY-MM-DD-slug.md
_projects/         Portfolio projects (a Jekyll collection)
_drafts/           Templates for new posts and projects
about.md           About page
portfolio.md       Portfolio page
_layouts/          Page templates (default, home, page, post, compress)
_includes/         Partials (header, footer, post rows, icons, roman numerals, ...)
_sass/codex/       Styles (tokens, layout, prose); entry point is assets/css/main.scss
pencil/            Design source (Pencil), not published
assets/uploads/    Images and PDFs used in content, including the CV
admin/             Netlify CMS (Decap) editor, available at /admin
```

## Writing content

### Option A: edit the Markdown files

Copy `_drafts/post-template.md` into `_posts/` (or `_drafts/project-template.md` into `_projects/`) and rename it to `YYYY-MM-DD-your-slug.md`. These front-matter fields matter most:

```yaml
---
layout: post
category: blog          # use "project" for files in _projects/
title: My Post
date: 2024-01-01 12:00
description: One-line summary shown in listings and SEO
tag: [gamedev, ai]
image: /assets/uploads/some-image.png
headerImage: false      # true shows `image` as a banner
author: ricardorodrigues
externalLink: false
hidden: false           # true keeps it out of listings but still reachable by URL
---
```

Put images in `assets/uploads/` and reference them as `/assets/uploads/file.png`.

### Option B: use the CMS

Go to <https://colorcrow.me/admin> and log in with GitHub. The editor runs in editorial-workflow mode, so every change becomes a pull request (`cms/...` branch) that you merge to publish. The collections and fields are defined in `admin/config.yml`.

After merging CMS changes, run `git pull` before you edit locally.

## Updating the résumé

The nav's *Résumé* link always points to `assets/uploads/cv-ricardo-rodrigues.pdf`, which is set by `resume-url` in `_config.yml`. You never need to rename anything. Edit your CV wherever you keep it, then run:

```bash
bundle exec rake cv                              # copies from the default source path in the Rakefile
bundle exec rake cv CV_SOURCE=~/path/to/cv.pdf   # or from any other file
```

Then commit and push the updated PDF.

## Deployment

Pushing to `gh-pages` is the whole deployment. GitHub Pages builds the site and serves it on the custom domain set in `CNAME`. There's no CI or build step to maintain. Pages only allows its own whitelisted plugins, so check that a plugin is supported before adding it to the `Gemfile`.

## Credits

Based on [Indigo](https://github.com/sergiokopplin/indigo) by Sérgio Kopplin ([MIT License](https://kopplin.mit-license.org/)). The original theme FAQ is in [FAQ.md](FAQ.md).
