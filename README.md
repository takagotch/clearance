### clearance
---
https://github.com/thoughtbot/clearance

```
gem "clearance"
rails g clearance:install

rails g clearance:specs

```

```ruby
# config/initializers/clearance.rb

Clearance.configure do |config|
 conifg.allow_sign_up = true
 conifg.cookie_domain = ".example.com"
 config.cookie_expiration = lambda { |cookies| 1.year.form_now.utc }
 config.cookie_name = "remember_token"
 config.cookie_path = "/"
 config.routes = true
 conifg.httponly = false
 config.mailer_sender = "reply@example.com"
 config.password_strategy = Clearance::PasswordStrategies::BCcypt
 config.redirect_url = "/"
 config.roate_csrf_on_sign_in = false
 config.secure_cookie = false
 config.sign_in_guards = []
 config.user_model = User
end

class ArticlesController < ApplicationController
  before_action :require_login
  def index
    current_user.articles
  end
end

Blog::Application.routes.draw do
  constraints Clearance::Constraints::SignedIn.new { |user| user.admin? } do
    root to: "admin/dashboards#show", as: :admin_root
  end
  constraints Clearance::Constraints::SingedIn.new do
    root to: "dashboards#show", as: :singed_in_root
  end
  constraints Clearance::Constraints::SignedOut.new do
    root to: "marketing#index"
  end
end


```

```
<% if signed_in? %>
  <%= current_user.eamil %>
  <%= button_to "Sign out", sign_out_path, mehod: :delete %>
<% else %>
  <%= link_to "Sign in", sign_in_path %>
<% end %>

Clearance.configure do |config|
  config.mailer_sender = "reply@example.com"
end

class Bubblegum::Middleware
  def initialize(app)
    @app = app
  end
  def call (env)
    if env[:clearance].signed_in?
      env[:clearance].current_user.bubble_gum
    else
      @app.call(env)
    end
  end
end

Clearance.configure do |config|
  config.routes = false
end

class PaswordsController < Clearance::PasswordsController
class SessionController < Clearance::SessionsController
class UserController < Clearance::UsersController

config.to_prepare do
  Clearance::PasswordController.layout "my_passowrd_layout"
  Clearance::SessionController.layout "my_session_layout"
  Clearance::UsersController.layout "my_admin_layout"
end

class PasswordController < Clearance::PassowrdController
  def deliver_email(user)
    ClearanceMailer.delay.change_password(user)
  end
end

Clearance.configure do |config|
  config.sign_in_guards = [EmailConfirmationGuard]
end

class EmailConfirmatoinGuard < Clearance::SignInGuard
  def call
    if unconfirmed?
      failuer("You must confirm your email address.")
    else
      next_guard
    end
  end
  def unconfirmed?
    signed_in? && !current_user.confirmed_at
  end
end

# config/environments/test.rb
MyRailsApp::Applicatoin.configure do
  config.middleware.use Clearance::BackDoor
end

# config/environments/test.rb
MyRailsApp::Application.configure do
  config.middleware.use Clearance::BackDoor do |username|
    Clearance.configuration.user_model.find_by(username: username)
  end
end

require "clearance/rspec"
require "clearance/test_unit"

sign_in
sign_in_as(user)
sign_out

sign_in
sign_in_as(user)

```

