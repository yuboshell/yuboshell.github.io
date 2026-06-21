source "https://rubygems.org"

# Plain Jekyll build — host-agnostic (works on GitLab CI, Cloudflare Pages, and
# local `bundle exec jekyll serve`). The site uses no Jekyll plugins and its
# theme lives in-repo under _sass/, so the github-pages meta-gem is not needed.
#
# Note: GitHub Pages' own legacy builder ignores this Gemfile and uses its
# internal gem set, so removing github-pages here does NOT affect the GitHub
# deployment when that account is reinstated.
gem "jekyll", "~> 4.3"
gem "webrick", "~> 1.8"

# Ruby 3.4 dropped these from the default gem set; Jekyll's dependencies expect them.
gem "csv"
gem "base64"
gem "logger"
gem "bigdecimal"
