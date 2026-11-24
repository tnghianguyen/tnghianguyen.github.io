Here is a personal blog built by Jekyll and hosted by Github Pages.

## Technologies used

### Bootstrap 4.3.1
### Jekyll

Currently, this site has been almost completed. The posts in the directory are experimental.

## Local development and security checks

Use a supported Ruby release (Ruby 3.3 or newer, with its latest security patches)
and Bundler 2.6.8. Install the locked dependencies with `bundle install`.

- Build: `bundle exec jekyll build`
- Preview locally: `bundle exec jekyll serve`
- Check Ruby dependencies against current advisories: `bundle exec rake security`
- Generate tag pages: `python3 scripts/tag_generator.py`

The Node package only provides command shortcuts; the website has no Node
dependencies. Unused linting and theme-release tools have been removed. Generated
site output and local caches should not be committed. GitHub Actions checks the
Ruby dependencies and builds the site, and Dependabot checks for updates weekly.

Production deployment uses the `Deploy website` GitHub Actions workflow and the
versions in `Gemfile.lock`. In repository Settings → Pages, the build source must
be **GitHub Actions**. The built-in Pages Jekyll builder uses its own bundled
plugins and does not honor this site's locked security updates.
