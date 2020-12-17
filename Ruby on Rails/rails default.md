# Rails 기본 설정

*   `rails new [project name] --skip-webpack-install --skip-javascript` 입력. 실행
    *   자바와 웹팩을 제외하고 프로젝트 생성
*   Gemfile 복사

```ruby
source 'https://rubygems.org'
git_source(:github) { |repo| "https://github.com/#{repo}.git" }

ruby '2.6.3'

# Bundle edge Rails instead: gem 'rails', github: 'rails/rails'
gem 'rails', '~> 6.0.2', '>= 6.0.2.1'
# Use sqlite3 as the database for Active Record
gem 'sqlite3', '~> 1.4'
# Use Puma as the app server
gem 'puma', '~> 4.1'
# Use SCSS for stylesheets
gem 'sass-rails', '>= 6'
# Use Uglifier as compressor for JavaScript assets
gem 'uglifier', '~> 4.2'
# Use CoffeeScript for .coffee assets and views
gem 'coffee-rails', '~> 5.0'

# For Jquery pause, When use turbolinks
gem 'jquery-turbolinks', '~> 2.1'
# Turbolinks makes navigating your web application faster. Read more: https://github.com/turbolinks/turbolinks
gem 'turbolinks', '~> 5.2', '>= 5.2.1'
# Build JSON APIs with ease. Read more: https://github.com/rails/jbuilder
gem 'jbuilder', '~> 2.7'
# Use Redis adapter to run Action Cable in production
# gem 'redis', '~> 4.0'
# Use Active Model has_secure_password
# gem 'bcrypt', '~> 3.1.7'

# Use Active Storage variant
# gem 'image_processing', '~> 1.2'

# Reduces boot times through caching; required in config/boot.rb
gem 'bootsnap', '>= 1.4.2', require: false

group :development, :test do
  # Call 'byebug' anywhere in the code to stop execution and get a debugger console
  gem 'byebug', platforms: [:mri, :mingw, :x64_mingw]
end

group :development do
  # Access an interactive console on exception pages or by calling 'console' anywhere in the code.
  gem 'web-console', '>= 3.3.0'
  gem 'listen', '>= 3.0.5', '< 3.2'
  # Spring speeds up development by keeping your application running in the background. Read more: https://github.com/rails/spring
  gem 'spring'
  gem 'spring-watcher-listen', '~> 2.0.0'
  gem 'rails_db'
end

group :test do
  # Adds support for Capybara system testing and selenium driver
  gem 'capybara', '>= 2.15'
  gem 'selenium-webdriver'
  # Easy installation and use of web drivers to run system tests with browsers
  gem 'webdrivers'
end

# Windows does not include zoneinfo files, so bundle the tzinfo-data gem
gem 'tzinfo-data', platforms: [:mingw, :mswin, :x64_mingw, :jruby]

# Use Design Framework for Front-End styling your web application
gem 'jquery-rails'
gem 'sassc-rails', '~> 2.1', '>= 2.1.2'
gem 'font-awesome-rails', '~> 4.7', '>= 4.7.0.5'

gem 'impressionist'

gem 'kaminari'

# For user Email send
gem 'mail_form'

# User Log in and Log out
gem 'devise'
gem 'devise-i18n'%
```

*   ### CSS 프레임 워크

    *   Bootstrap

        *   [version 3](https://www.w3schools.com/bootstrap/)
        *   version 4
            *   [w3schools](https://www.w3schools.com/bootstrap4/default.asp)
            *   [Home](https://getbootstrap.com/docs/4.0/getting-started/introduction/)
        *   Gemfile

        ```ruby
        // version 3
        gem 'bootstrap-sass', '~> 3.4', '>= 3.4.1'
        
        // version 4
        gem 'bootstrap', '~> 4.4.1'
        ```

        *   application.scss

        ```scss
        // "bootstrap-sprockets" must be imported before "bootstrap" and "bootstrap/variables"
        @import 'bootstrap-sprockets';
        @import 'font-awesome';
        @import 'bootstrap';
        ```

        *   application.js

        ```js
        //= require jquery
        //= require bootstrap-sprockets
        //= require jquery_ujs
        //= require_tree .
        ```

        

    *   Semantic UI

        *   Gemfile

        ```ruby
        gem 'semantic-ui-sass', '~> 2.4', '>= 2.4.2.0'
        ```

        *   application.scss

        ```scss
        @import 'semantic-ui';
        @import 'font-awesome';
        ```

        *   application.js

        ```js
        //= require jquery
        //= require semantic-ui
        //= require jquery_ujs
        //= require_tree .
        ```

    *   MaterializeCSS

        *   Gemfile

        ```ruby
        gem 'materialize-sass'
        ```

        *   application.scss

        ```scss
        @import 'https://fonts.googleapis.com/icon?family=Material+Icons';
        @import 'materialize';
        ```

        *   application.js

        ```js
        //= require jquery
        //= require materialize
        or
        //= require materialize-sprockets
        //= require jquery_ujs
        //= require_tree .
        ```

    *   `bundle install` 입력. 실행

*   ### views

    *   layouts

        *   application.html.erb
            *   javascript_include_tag에 `'data-turbolinks-trank': 'reload'`를 적용하지 않은 이유

        ```html
        <%= stylesheet_link_tag    'application', media: 'all', 'data-turbolinks-track': 'reload' %>
        <%= javascript_include_tag 'application' %>
        <meta name="viewport", content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=0">
        ```
```
        
        *   터보링크는 javascript 나 css 를 미리 받아 옴으로써 다시 리로딩 하지 않아도 된다. 그렇게 되면 웹의 속도가 향상되지만 한번만 로드 된다는 점에서 자바스크립트에 문제가 생긴다. 예를 들어 HTML에 태그 추가가 두번 된다거나 클릭 이벤트가 되지 않는다거나 외부 api를 이용할수 없는 등이 있다. 물론 페이지를 새로고침 하면 되지만, 그 밖의 심각한 문제들도 있기 때문에, SPA 프로젝트가 아니라면 자바 스크립트 파일에서 적용하지 않는 것을 권장한다.	


```