---
layout: post
title:      "Sinatra Portfolio Project"
date:       2018-06-28 20:34:24 +0000
permalink:  sinatra_portfolio_project
---


The Sinatra Portfolio Project focuses primarily on Sinatra and Active Record, requiring an app that uses both. Sinatra allows users to quickly create web applications and Active Record makes creating relational databases a breeze. Combining the two allowed me to set up a database with three models (Building, Resident, and ServiceRequest) and then let a user interact with that database through a web app. 

The key when setting up the database was to lay out how the models should relate to one another. I decided on a straightforward pattern- a Building has many Residents and a Resident belongs to a Building. Similarly, a Resident has many Service Requests and a Service Request belongs to a Resident. The logic behind this relationship is that the app could be used by the residents of a group of apartment buildings in a given city. 

To start things off, I looked up the top ten apartment buildings in San Francisco and used those names to create ten buildings in my seed file for this project. That way, when a resident signs up to use the web app, they can simply select the building they're living in. Once a resident is logged in, they can create, read, update, and delete service requests. A service request would theorhetically be something like, "my kitchen sink is leaking, someone will need to come repair it." The app's functionality could be expanded to include a message-sending funciton so that a building manager could receive all of the service reqeuests, but for now we're keeping it simple. 

In order to see a bit more about how the data is collected, and how the models relate to each other, I created a url path for the user to see all of the buildings and the usernames of residents in each building. Additionally, each building keeps a count of the number of reidents and service requests that it has. 

Since the url paths are all pretty straightforward, it would be easy for someone to replace their username with another's in the url. To prevent the wrong user from seeing another users' information, pages displaying user-specific data verify that the current user matches the user in the url first. If they dont match, the page will redirect to a neutral page like the homepage. There are similar protections for viewing and editing service requests. 

One interesting part of this project was validating user input from the signup form. For instance, a user would need to fill out each part of the form before the controller would accept a successful submission. Additionally, only new usernames could be accepted, in order to prevent duplicate usernames in the database. Fortunately, I was able to add some simple validations to the Resident class in the model folder (code below).

    validates :username,  uniqueness: true
    validates :username,  presence: true
    validates :name,  presence: true
    validates :building_id,  presence: true
    validates :apt_number,  presence: true
		
On the login page, the user's password would also need to be authenticated somehow. First, "has_secure_password" was added to the Resident class above the validations. Second, in the residents_controller  "post '/login' do" block , once @resident was established by searching for the username param, I was able to check for a correct password by writing "@resident.authenticate(params[:password])". If an incorrect password was found, a flash message would present ont he next page saying "Incorrect password, please try again."

All in all, it was a fun project with a lot of potential to do more with the idea. 
	

