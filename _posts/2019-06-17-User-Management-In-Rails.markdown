---
layout: post
title:  "Implementing User Management in Rails"
date:   2019-06-17 15:23:36 +0100
description: Third Post
---

Modern web applications often require some kind of system to enable users to register, log in and log out. Creating all these files manually can be a long process, and it’s likely that you might make an error somewhere. Devise is a Ruby gem that makes the process of adding this functionality extremely simple and easy. 

To begin, we must add the Devise gem to our gemfile (requires Rails 4.1+)

```
gem 'devise'
```

Now run ```bundle install``` to install the gem

We can now run the Devise generator

```
rails generate devise:install
```

Before we can begin using devise, we need to do three things

**1) Ensure that your application has a way to display error messages**

Visit your main application layout (**app/views/layouts/application.html.erb**)

A simple implementation for alerts can be done by adding the following code within the body tag

```erb
<body>
  <div class="container">
    <p class="alert"><%= alert %></p>
    <%= yield %>
  </div>
</body>
```

**2) Configure a development environment**

Visit your development environment file (**config/environments/development.rb**) and add the following code (you might want to change the port number and host depending on your situation).
```rb
config.action_mailer.default_url_options = { host: 'localhost', port: 3000 }
```

**3) Have a root (default address page) in your routes file**

Visit your root file (**config/routes.rb**) and add a root. You can generate the pages for an index page using ```rails g controller Pages index```, which will create a pages controller with an index function as well as an index view (**app/views/pages/index.html.erb**)

```rb
root 'pages#index'
```

Now we need to generate a Model for the application’s users, and configure it with the Devise modules

```
rails g devise User
```
_Note: You can replace 'User' with any other type of account if you wish, such as 'Admin'._

Now we must migrate the database

```
rails db:migrate
```

We can also use Devise to generate the views for the users. This will create the basic views for the Devise user functionality (registration, sign in and update profile)

```
rails g devise:views
```

We’re going to add Bootstrap to our Rails application at this point to make everything look a little nicer. You can skip this part if you like

Add these gems to your gemfile
```
gem 'bootstrap', '~> 4.3.1'
gem 'jquery-rails'
```

Now run ```bundle install```

Navigate to your application's scss file I DONT KNOW HOW ELSE TO NAME THIS (**app/assets/stylesheets/application.scss**) and add

```scss
@import "bootstrap";
```
_Note: if you have no application.scss but instead have application.css, rename the file by running the following command in the terminal
```$ mv app/assets/stylesheets/application.css app/assets/stylesheets/application.scss```_

Bootstrap 4 is now installed in your Rails application.

I also like to change the default method for signing out of the Rails application. By default, the method is :delete, however sometimes an incorrect request is sent if your javascript is not set up completely correct meaning that the log out function doesn't work correctly. To do this, visit your Devise initialiser (**/config/initializers/devise.rb**). Change
```rb
config.sign_out_via = :delete
```
To 
```rb
config.sign_out_via = [:delete, :get]
```

Now we have the models, views and controllers to register, log in, log out and update Users. Now we’re going to add some navigation which differs depending on whether a user is signed in or not. To do this, we’re going to utilise a devise helper user_signed_in?
_Note: the user part of the helper depends on the model that you generated. If you generated an admin model, the helper would be admin_signed_in?_

Within our main application layout file (**app/views/layouts/application.html.erb**), add the following within the body above your alert messages

```erb
<nav class="navbar navbar-expand-lg navbar-light bg-light">
  <div class="container">
    <button class="navbar-toggler" type="button" data-toggle="collapse" data-target="#navbarTogglerDemo03" aria-controls="navbarTogglerDemo03" aria-expanded="false" aria-label="Toggle navigation">
      <span class="navbar-toggler-icon"></span>
    </button>
    <a class="navbar-brand" href="/">Tutorial</a>

    <div class="collapse navbar-collapse" id="navbarTogglerDemo03">
      <ul class="navbar-nav mr-auto mt-2 mt-lg-0">
        <li class="nav-item">
          <%= link_to "Home", root_path, class: "nav-link" %>
        </li>
      </ul>
      <ul class="navbar-nav navbar-right my-2 my-lg-0">
        <% if user_signed_in? %>
          <li class="nav-item">
            <%= link_to "Log out", destroy_user_session_path, class: "nav-link" %>
          </li>
          <li class="nav-item">
            <%= link_to "Edit Profile", edit_user_registration_path, class: "nav-link" %>  
          </li>
        <% else %>  
          <li class="nav-item">
            <%= link_to "Register", new_user_registration_path, class: "nav-link" %>
          </li>
          <li class="nav-item">
            <%= link_to "Log in", new_user_session_path, class: "nav-link" %>
          </li> 
        <% end %>
      </ul>
    </div>
  </div>
</nav>
```

Now if you run ```rails s```, and visit [http://localhost:3000/][localhost], you will be able to login in to your site using Devise. 

[localhost]: http://localhost:3000