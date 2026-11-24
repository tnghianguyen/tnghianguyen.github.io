# Trung Nghia Nguyen — Personal Website

Source for my personal academic website, including research, teaching, and
mathematics posts.

**Website:** [www.tnghia.com](https://www.tnghia.com/)

Built with Jekyll, Liquid, and Sass, with MathJax for mathematical notation.
GitHub Actions builds the site from locked Ruby dependencies and deploys it to
GitHub Pages.

## Run locally

Use Ruby 3.3, matching the deployment workflow, and Bundler 2.6.8. Python 3 is
needed only for generating tag pages. Node.js is not required to build the site.

```sh
git clone https://github.com/tnghianguyen/tnghianguyen.github.io.git
cd tnghianguyen.github.io
gem install bundler -v 2.6.8
bundle _2.6.8_ install
bundle exec jekyll serve
```

Open [localhost:4000](http://localhost:4000/). Restart the preview server after
changing `_config.yml`.

To create a production build in `_site/`:

```sh
JEKYLL_ENV=production bundle exec jekyll build
```

## Update content

| Location | Purpose |
| --- | --- |
| `index.html` | About and contact information |
| `research.html` | Research, talks, and academic activities |
| `teaching.html` | Teaching information |
| `_posts/` | Dated mathematics and seminar posts |
| `tags/` | Generated tag pages |
| `_layouts/` and `_includes/` | Shared page templates and components |
| `_sass/` and `assets/` | Stylesheets and browser scripts |
| `img/` | Images |
| `_config.yml` | Site metadata, navigation, and Jekyll settings |

Create posts directly in `_posts/` using `YYYY-MM-DD-title.md` filenames and YAML
front matter. For example:

```yaml
---
layout: post
title: My mathematics post
tag: [algebra, geometry]
mathjax: true
---
```

After adding or changing post tags, regenerate the tag pages:

```sh
python3 scripts/tag_generator.py
```

This replaces the Markdown files in `tags/`; commit the regenerated pages with
the posts. Tag generation is not automatic in CI.

The templates load `assets/js/main.min.js`. If editing `assets/js/main.js`, keep
the minified file in sync. The optional `npm run minify` shortcut requires a
separately installed Closure Compiler.

## Validate changes

| Command | What it checks |
| --- | --- |
| `bundle exec jekyll build` | Generates the website |
| `bundle exec rake test` | Builds the site and checks HTML, assets, and links |
| `bundle exec rake security` | Refreshes RubySec advisories and audits locked Ruby dependencies |

Link checks and advisory updates require network access. Commit source files and
`Gemfile.lock`; generated `_site/` output and local caches are ignored.

## Deployment and security

Pushing to `main` runs the [Deploy website workflow](.github/workflows/pages.yml).
It audits the dependencies, builds with the versions in `Gemfile.lock`, and
deploys the resulting static files after a successful build. The workflow can
also be started manually from the Actions tab on `main`.

In **Settings → Pages → Build and deployment**, keep the source set to
**GitHub Actions**. This ensures production uses the locked dependencies rather
than the separate plugin versions bundled with the legacy Pages builder.
Keep the custom domain configured in **Settings → Pages** and keep `url` in
`_config.yml` aligned with it.

The [Security and build workflow](.github/workflows/security.yml) audits Ruby
dependencies and builds the site for pull requests and pushes to `main`.
[Dependabot](.github/dependabot.yml) checks for dependency and action updates
weekly. Dependabot alerts, CodeQL, and secret scanning are enabled in the
repository; current findings are available in the
[security dashboard](https://github.com/tnghianguyen/tnghianguyen.github.io/security).

## License

See [LICENSE.md](LICENSE.md) for the MIT license.
