---
layout: post
title:      "Rails Project"
date:       2018-07-26 16:12:40 -0400
permalink:  rails_project
---

*The Movie Rental web application allows customers to log in to the platform and select a movie to "rent". They can sign up for a new account or log in with Facebook. Once logged in, the customer can view a list of movies, see further details about a given movie, and rent it. Once the movie is rented, it appears on the "My Rentals" page and, from there, the customer can choose to return it. After the customer returns the movie, they can add a famous quote to it for all the other customers to see. The web app will only allow a customer to rent a movie if they are old enough to watch it (based on the MPAA rating system).*

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

My favorite piece of this project was the join table (Rentals) connecting Customers and Movies. Other than facilitating the many-to-many relationiship for Customers/Movies, it's most important features was its `status` attribute. It allowed me to set the status to either "checked out" or "returned" depending on what action the custsomer had taken. I created a method `rent_movie` in the Rental class to check out a movie and made a return button on the My Rentals page for each movie a customer had rented. I made a few other methods in the Rental class- two that use ActiveRecord to scope a list of checked out movies or past movie rentals, and one that verifies that a customer is old enough to watch a certain movie (according to the MPAA rating). 

