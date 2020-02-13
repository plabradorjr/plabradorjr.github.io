---
layout: post
title:      "Sinatra Project 💔"
date:       2020-02-13 03:07:38 +0000
permalink:  sinatra_project
---


For this project, I built an open-content collaborative database.  A simple content management system [(CMS)](https://en.wikipedia.org/wiki/Content_management_system).


![project landing page](https://raw.githubusercontent.com/plabradorjr/blog_images/master/surgi_app_index.png)


# Purpose 
<hr>
### Problem Overview

This app is built for new operating room nurses and surgical techs (orientees and travelers) working at my current job. It's not built for the masses. Target audience of about 50 or so people. That's it. Within our Operating Room (OR) department, there are millions worth of medical supplies and equipments stored in multiple different shelves, rooms, and building floor-levels. None of the storage areas are exactly identical in layouts. None of the storage areas have aisle numbers or ways to easily find things. For newer staffs, it becomes very easy to get lost trying to find equipments. 

Instead of focusing on patient care or other medical related tasks, we continually lose time trying to find simple items. There are no documentations to where the supplies are located. It's a simple problem that can be solved with a ruthlessly minimalistic CMS. Our OR department will always have new hires that can benefit from a search engine and database to effectively find a specific item. 

### Goal

The goal is to help nurses and surgical techs grow, regardless of experience level . The more we contribute and organize our information, the better off we'll be. More data is not always better, what we are really looking for is forward-motion. 

>“Train people well enough so they can leave, treat them well enough, so they don't want to”. — Richard Branson


>“We don't rise to the level of our expectations, we fall to the level of our training.” ― Archilochus

# Design overview
<hr>

SurgiApp is deliberately designed so that collaboration is key to its usefulness. Anyone can edit any entries. Without other peoples' contributions, this app leads nowhere, and information will remain outdated. 

If a user is loged-in, they can edit any entries. However, only the original content creator can completely delete it.

A user also has a "user page" and only they can edit their own profile bio.

### Schema

To build the schema, there are only two tables, a `users table` and a `notes table`.

A `user` has_many `notes`.

And `notes` belongs_to `user`.

### Front-End

I used Bootstrap for CSS. 

### Conventional RESTful urls

`/users` => shows all registered users

`/user/:username` => shows individual user

`/note` => shows all notes

`/note/:id` => shows individual notes


### Gems

The gems are the basics:

```
gem "sinatra"
gem "activerecord", '<= 5.1'
gem "sinatra-activerecord"
gem "rake"
gem "bcrypt"
gem "require_all"
gem "capybara"
gem "pry"
gem 'sqlite3', '~> 1.3.6'
gem 'shotgun'

group :development do
  gem "tux"
end

```

## Login Vulnerabilities

While developing the login functionality, I noticed a lot of problems and vulnerabilities if the username is allowed to be case sensitive *and* allowed to use special characters. 

For instance, I can have multiple users with names like 1) `Kanye` 2) `kanYE` 3) `kaNyE` and so on. It could be very confusing which one is which. Excluding special characters is also very helpful to have RESTful username urls. A username who sign up with names that include `!$%` and any other special characters could cause url breakdowns based on my current RESTful url code. 

I found this method with regex  to allow only words, underscore and numbers. Any other special characters will return false. I included this on the application_controller helper method:

```
def valid_login?(str)
      return true if (/^\w*$/.match(str))
      return false
end
```

usage:
```
> valid_login?("testing") 
  true
> valid_login?("a b")
  false
> valid_login?("a%")
  false

```


I also passed all the username parameters to be stored in the databse as downcase, therefore making all username non-case sensitive. 

So far, I was **not** able to break this signup code:

```
 post '/signup' do
    downcase_name = params[:username].downcase
    downcase_email = params[:email].downcase
    username_taken = User.find_by(:username => downcase_name)
    email_taken = User.find_by(:email => downcase_email)
		
    if username_taken
        @error_message = "Sorry, that username is already taken."
        erb :'/users/error_message'
    elsif email_taken
        @error_message = "Sorry, that email is already taken."
        erb :'/users/error_message'
    elsif !valid_login?(params[:username])
        @error_message = "Sorry, special characters are not allowed in username. Choose only words, underscore and numbers. Please try again."
        erb :'/users/error_message'
    elsif params[:username] == "" || params[:email] == "" || params[:password] == ""
        @error_message = "Sorry, all fields must be filled out. Try again."
        erb :'/users/error_message'
    else
      @user = User.new(:username => downcase_name, :email => downcase_email, :password => params[:password])
      @user.save
      session[:user_id] = @user.id
      redirect to '/home'
    end
 end
```


<hr>
# Break my site 💔, I want you to.

Seriously. I really want to make this app to be safely operational. 

Here is the live beta website:


[https://surgi-app-v0.herokuapp.com](https://surgi-app-v0.herokuapp.com/home)


Shoutout to @sunny from learn.co slack for making [this awesome video](https://www.youtube.com/watch?v=m_tRqz9wu_0). It helped me deploy my project to Heroku.

If you can break it and find any vulnerabilities, please reach me on twitter @plabradorjr

I'm sure we will learn more about better login/signup feature as we move along the curriculum. I'm excited to continually develop this app as I learn more features.


Any feedback is appreciated. Thanks! @pancho on Learn.co Slack channel. It'd be a pleasure to hear from you. 



