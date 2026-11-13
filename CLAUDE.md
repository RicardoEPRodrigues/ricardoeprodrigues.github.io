# CLAUDE.md

Personal website (colorcrow.me) built with Jekyll on the Indigo theme and served by GitHub Pages from the `gh-pages` branch. `gh-pages` is the default branch, and pushing to it deploys the site.

## Commands

- `bundle install`: install gems. Requires Ruby 2.7.6 (see `.ruby-version`, managed with rbenv).
- `bundle exec jekyll serve --livereload --drafts`: dev server on http://localhost:4000.
- `bundle exec jekyll build`: build into `_site/`. Use this to check that a change renders.
- `bundle exec rake`: run html-proofer on `_site/` (build first).

## Constraints

- The site is built by **GitHub Pages**, not by us. Only plugins on the Pages whitelist work, and Jekyll is pinned to 3.9 by the `github-pages` gem. Don't add plugins or Jekyll 4 features.
- `Gemfile.lock` and `_site/` are gitignored. Don't commit them.
- `pagination.enabled` is `false` on purpose because `jekyll-paginate-v2` isn't supported on Pages.
- `_config.yml` changes need a server restart to take effect.
- The `compress` layout minifies HTML. Inline `//` JS comments in layouts or includes will break pages, so use `/* */`.

## Content

- Posts go in `_posts/YYYY-MM-DD-slug.md` with `category: blog`. Projects go in `_projects/` with `category: project`. Both use `layout: post` and `author: ricardorodrigues`. Templates are in `_drafts/`.
- Media goes in `assets/uploads/`, referenced as `/assets/uploads/...`.
- Content is also edited through Netlify CMS (`admin/`, editorial workflow), which opens PRs from `cms/...` branches. If you rename front-matter fields or collections, update `admin/config.yml` to match.
- `about.md` and `portfolio.md` are managed by the CMS as markdown bodies.

## Styling

- Colours and the theme mode come from `_config.yml` (`accent-color`, `background`, `dark-theme`). They're injected into SCSS in `_layouts/default.html`.
- Styles live in `_sass/` and `_includes/style*.scss`. Icons come from the Font Awesome kit script in `_layouts/default.html`.
