source "https://rubygems.org"

# Core Jekyll and plugins
gem "jekyll", "~> 4.3.0"
gem "jekyll-feed", "~> 0.17"
gem "jekyll-seo-tag", "~> 2.8"
gem "jekyll-sitemap", "~> 1.4"

# If you have any plugins, put them here!
group :jekyll_plugins do
  # Plugins can be listed here if needed, but avoid duplicates
end

# Windows and JRuby does not include zoneinfo files, so bundle the tzinfo-data gem
# and associated library.
platforms :windows, :jruby do
  gem "tzinfo", ">= 1", "< 3"
  gem "tzinfo-data"
end

# Performance-booster for watching directories on Windows
gem "wdm", "~> 0.1.1", :platforms => [:windows]

# Lock `http_parser.rb` gem to `v0.6.x` on JRuby builds since newer versions of the gem
# do not have a Java counterpart.
gem "http_parser.rb", "~> 0.6.0", :platforms => [:jruby]

# Use `debug` to add debugging support
gem "debug", platforms: %i[ mri windows ] 

gem "csv"
gem "logger" 
gem "base64" 