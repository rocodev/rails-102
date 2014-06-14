# Bundler

[Bundler](http://gembundler.com/) 是一套可以解決外部工具及其相依關係的好用工具，現在基本上所有以 Ruby 開發的工具，基本上都是使用這套工具管理專案上的套件相依關係。

Bundler 依據 `Gemfile` 這個檔案安裝以及判斷套件相依性。`bundle install` 可以幫我們安裝 project 裡面需要的正確的 Gem 版本。


Rails 中的 Gemfile 內會是長這樣

``` ruby 
source 'https://rubygems.org'

# Bundle edge Rails instead: gem 'rails', github: 'rails/rails'
gem 'rails', '4.0.0'

# Use sqlite3 as the database for Active Record
gem 'sqlite3'

# Use SCSS for stylesheets
gem 'sass-rails', '~> 4.0.0'

# Use Uglifier as compressor for JavaScript assets
gem 'uglifier', '>= 1.3.0'

# Use CoffeeScript for .js.coffee assets and views
gem 'coffee-rails', '~> 4.0.0'

# See https://github.com/sstephenson/execjs#readme for more supported runtimes
# gem 'therubyracer', platforms: :ruby

# Use jquery as the JavaScript library
gem 'jquery-rails'

# Turbolinks makes following links in your web application faster. Read more: https://github.com/rails/turbolinks
gem 'turbolinks'

# Build JSON APIs with ease. Read more: https://github.com/rails/jbuilder
gem 'jbuilder', '~> 1.2'

group :doc do
  # bundle exec rake doc:rails generates the API under doc/api.
  gem 'sdoc', require: false
end

# Use ActiveModel has_secure_password
# gem 'bcrypt-ruby', '~> 3.0.0'

# Use unicorn as the app server
# gem 'unicorn'

# Use Capistrano for deployment
# gem 'capistrano', group: :development

# Use debugger
# gem 'debugger', group: [:development, :test]

```

## 常見 Bundler 指令

* `bundle check` : 檢查此專案的套件是否漏失
* `bundle install` : 安裝此專案所需要的套件


在 clone 下一個專案後，我們先會使用 `bundle install` 這個指令確定這個專案裡面，套件都被正確安裝了，才能繼續啟動專案。