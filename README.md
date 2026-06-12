# augforce.github.io

Personal portfolio for Michael Augustine — AI Conductor.
Built with [Jekyll](https://jekyllrb.com/) and hosted on GitHub Pages.

## Editing content

No HTML needed for the common cases:

- **Projects** → `_data/projects.yml` (one entry per card)
- **Skills** → `_data/skills.yml`
- **Contact details, title, tagline** → `_config.yml`

Layout/markup lives in `_layouts/default.html` and `_includes/*.html`.
Styling is `assets/css/style.css`; interactions are `assets/js/main.js`.

## Local preview (optional)

Requires Ruby + Bundler:

```sh
bundle install
bundle exec jekyll serve
# open http://127.0.0.1:4000
```

## Deploy

Push to `main`; GitHub Pages builds and serves at https://augforce.github.io/.
