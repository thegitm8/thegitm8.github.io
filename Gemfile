source "https://rubygems.org"
ruby RUBY_VERSION

require 'json'
require 'open-uri'
versions = JSON.parse(open('https://pages.github.com/versions.json').read)

gem 'github-pages', '>= 207', versions['github-pages'], group: :jekyll_plugins


# If you have any plugins, put them here!
group :jekyll_plugins do
   gem "jekyll-feed", "~> 0.9", ">= 0.9.2"
end

# Windows does not include zoneinfo files, so bundle the tzinfo-data gem
# gem 'tzinfo-data', platforms: [:mingw, :mswin, :x64_mingw, :jruby]

# gem 'jekyll-compose', group: [:jekyll_plugins]
