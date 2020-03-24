# [DEPRECATED!]
## Rails Modern UI Starter Template
![Schema](https://raw.githubusercontent.com/sadikay/rails-modern-ui/master/public/modernist.png?token=AIE99TZIkj-hjo186CFGGxpS8-f025J3ks5aXw4uwA%3D%3D)

### Quick Install
```
git clone https://github.com/sadikay/rails-modern-ui.git
```
### Setup From Zero
#### Create Rails App
 `rails new rails_modern_app --skip-coffee --skip-sprockets --skip-turbolinks --webpack --database=mysql  -T`

#### Browser Config
 Process your code to be cross-browser compliant

 `touch .browserslistrc`

 and add and add a single line: `> 1%`

#### Application.rb

 ```ruby
 # config/application.rb
  config.generators do |g|
    g.test_framework  false
    g.stylesheets     false
    g.javascripts     false
    g.helper          false
    g.channel         assets: false
  end
 ```

#### Frontend Config
 * Remove the `app/assets` folder.
 * Move `javascript` folder from `app/javascript` to root dir and rename it to `frontend`. Make sure the path `frontend/packs/application.js` exist.
 * Go to `application.html.erb` and replace `javascript_include_tag "application"` with `javascript_pack_tag "application"`
 * Replace `stylesheet_link_tag 'application', media: 'all'` with `stylesheet_pack_tag 'application'`
 * Go To `config/webpacker.yml` and configure `source_path: frontend` line.

#### Install Haml
 Add this line to Gemfile and bundle.

 ` gem "haml-rails", "~> 1.0" `

 Convert erb to haml with:
 ```
 rails generate haml:application_layout convert

 HAML_RAILS_DELETE_ERB=true rake haml:erb2haml
 ```

#### Controller Config
 Tell frontend path to controller:
 ```ruby
  # app/controllers/application_controller.rb
  class ApplicationController < ActionController::Base
    protect_from_forgery with: :exception
    prepend_view_path Rails.root.join("frontend")
  end
 ```

#### Starting Dev Server
 * `touch Procfile` and put inside
  ```
   server: bin/rails server
   assets: bin/webpack-dev-server
  ```

 * Install  [hivemind](https://github.com/DarthSim/hivemind) and configure it.

 * Run `rake db:create` && `rake db:migrate`

#### Source
 https://evilmartians.com/chronicles/evil-front-part-1
