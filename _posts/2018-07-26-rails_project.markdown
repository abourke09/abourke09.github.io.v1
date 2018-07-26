---
layout: post
title:      "Rails Project"
date:       2018-07-26 20:12:39 +0000
permalink:  rails_project
---


The Rails Portfolio Project has been a nice opportunity to put some new tools to use. It's gratifying to be able to connect relational databases with user logins and display all of that through a few different page views. As with anything, the individual components only reach their full potential when used in concert with others.  

One of the biggest challenges with this project was organizing all of my code in a way that made sense. With controllers for the application, sessions, customers, rentals, movies, and famous quotes, the filetree started bulking up pretty quickly. I used four models in this project, which isn't really a lot, but it set the stage for a number of different views. Using MVC architecture for separation of concerns and standard naming conventions for files helped. 

Using a CustomersHelper module allowed me to abstract out a method called `check_for_age`, which helped reduce the amount of code logic I needed on my Customer show page. Similarly, adding a few helper methods in my Movie and Rental models cut down on the amount of logic and repetitious code in the controllers and views. 

The web app's login page features the standard input fields to sign in and an option to sign in with Facebook instead. I used Omniauth for login authentication and the Facebook Omniauth gem. It was interesting to incorporate 3rd party login because it required a bit more logic in the Session Controller `create` method (shown below). I used an `if` statement to check to see whether the customer logged in with Facebook or by typing in their own credentials. Authenticating the login params for a normal login is pretty straightforward, but the Facebook login was a little different. I was able to iterate through the `auth` params that the Omniauth Facebook gem made available and select `['info']['email']` to find (or create) the correct customer to login. For both types of logins, each respective code block ends by setting the session `customer_id` to the new instance of `@customer.id` .

```
  def create
    if request.env['omniauth.auth']
      @customer = Customer.find_or_create_by(email: auth['info']['email']) do |c|
        c.name = auth['info']['name']
        c.email = auth['info']['email']
        c.password = "0"
      end

      @customer.save
      session[:customer_id] = @customer.id
      redirect_to '/'
    else
      @customer = Customer.find_by(email: params[:customer][:email])

      if @customer && @customer.authenticate(params[:customer][:password])
        session[:customer_id] = @customer.id
        redirect_to customer_path(@customer)
      else
        redirect_to '/login'
      end
    end
  end
```
