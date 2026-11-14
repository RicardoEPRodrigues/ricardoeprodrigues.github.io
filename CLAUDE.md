# CLAUDE.md

Personal website (colorcrow.me) built with Jekyll (originally the Indigo theme, now a custom "Verdigris Codex" design) and served by GitHub Pages from the `gh-pages` branch. `gh-pages` is the default branch, and pushing to it deploys the site.

## Commands

- `bundle install`: install gems. Requires Ruby 2.7.6 (see `.ruby-version`, managed with rbenv).
- `bundle exec jekyll serve --livereload --drafts`: dev server on http://localhost:4000.
- `bundle exec jekyll build`: build into `_site/`. Use this to check that a change renders.
- `bundle exec rake`: run html-proofer on `_site/` (build first).
- `bundle exec rake cv`: copy the CV from `CV_SOURCE` (default path is in the `Rakefile`) to `assets/uploads/cv-ricardo-rodrigues.pdf`. Keep that target filename stable, because `resume-url` points at it.

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

- The design source is `pencil/design.pen` (open it with the Pencil MCP tools, never read it directly). Keep the site and the design in step.
- `assets/css/main.scss` is the stylesheet entry. It has front matter so Liquid can inject `accent-color`, `accent-color-dark`, `background`, `background-dark` and `dark-theme` from `_config.yml`. Every other colour is a CSS variable set in `_sass/codex/_tokens.scss`.
- Partials live in `_sass/codex/`. GitHub Pages compiles them with Ruby Sass, so avoid CSS `min()`/`max()` (they clash with Sass functions).
- Fonts: Grenze Gotisch (headings only), EB Garamond (text), Inter (small capitals), loaded from Google Fonts in `_layouts/default.html`. Social icons come from the Font Awesome kit, and UI glyphs from `_includes/icon.html`.
- Decoration must come from layouts and CSS, never from content: the drop cap is `::first-letter` on the first paragraph of `.prose`, `##` headings get the gilt underline, and an image with a title becomes a captioned plate (small script in `_layouts/default.html`).
- The woodcut crow is `assets/images/crow.svg`. It switches colours with `prefers-color-scheme` on its own.
- Home page copy (kicker, intro, featured work, works list) is front matter in `index.md`, edited in the CMS as "Home Page". Roman numerals come from `_includes/roman.html`.
