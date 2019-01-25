---
layout: post
title:      "Rails and Javascript Project"
date:       2019-01-25 20:14:26 +0000
permalink:  rails_and_javascript_project
---


Adding Javascript to a Rails webapp follows a fairly straightforward and intuitive pattern (once you've already done it, that is!). Once I integrated a small portion of JS, it was pretty clear I'd be able to follow the same approximate steps to add JS to the rest of the project. Having an Active Model Serialization JSON backend was critical to passing along the appropriate data to my JS file. One struggle I encountered was staying in control of the DOM, preventing automatic refreshes and redirects, and knowing when to allow for a single refresh of the page.

After generating serializers for each of the models, and adding their relationships to each serializer, the first step was to make sure I could access the appropriate data from JSON. These were a few of the most important routes for my app: 

	-'/movies.json'
	-'/movies/:id.json'
	-'/customers/:id.json'
	-'/customers/:id/rentals.json'

Once I saw that I could successfully access each of those JSON routes, I was able to outline an AJAX 'get' request for each of them. In the success function of the AJAX request, I could use the 'response' passed back to grab the data I needed from the JSON page and manipulate it to appear on my DOM how I wanted it. 

Before really diving into the deep end of JS/AJAX/JSON, it was helpful to have a sort of 'whiteboard' on my application.html.erb view. Since the plan was to inject all of my HTML onto the DOM at will, there had to be a good place to put it. My solution was to just create a div with the id of 'whiteboard' that I could fill up and clear again according to what I wanted displayed. 

Another crucial step near the beginning was staying in control of the DOM and preventing refreshes or rendering other urls. That meant paying close attention to the NavBar header on my application.html.erb view. To stay in control of the DOM, I created a function in my index.js file that would 'listen' for a click on my navbar. Then the function would determine which link was clicked, prevent the default redirect to a new page, and instead send the click action to a specific function in one of my JS files. It was helpful to organize these first few steps into one function called listenForNavClick(). 

Of course, none of this would have been possible without the mighty document.ready function. Since the document.ready function is loaded first, it was responsible for setting my currentUser() and calling listenFornavClick(). Otherwise, there would be no way to hijack the nav clicks and none of my JS would be able to run. 
	`$(function (){
		currentUser()
		listenForNavClick()
	})`
	
At this point,  I've described how my project uses document.ready, event listeners, AMS JSON data, and AJAX requests to pluck information from my database and make it available in my Javacsript files. In order to display that data on the DOM, constructor functions and protoype functions were both extremely valuable to create instances of each object and display HTML on the DOM in a readable format. But there are two other parts of my project that stand out as different from the rest: the currentUser() function and the check_for_age attribute of Customer. 
	
The check_for_age attribute was added to my Customer Serializer because I needed a way to display a statement like "According the the Motion Picture Association of America (MPAA), you are old enough to see movies with a rating of G, P, and PG-13." Of course the allowed rating is dependant on the age of the customer, and that logic was spelled out in my customer model under the check_for_age method. Since I couldn't access that method from my JS files, adding check_for_age to each instance of a customer gave me the ability to access the info through and AJAX JSON request. 

The currentUser() function was created so that I would have a way to access the current user's id at any time. First I created a route at get '/get_current_user' that pulled JSON data from the get_current_user method in the Customer Controller. The currentUser() function sent an AJAX get request to that url and returned the current user id by setting it in an item in sessionStorage. Since AJAX is asynchronous, it's not possible to simply set the id equal to a varible. SessionStorage allowed me to set the value of the id inside the AJAX request and then access it again outside of the request by calling sessionStorage.getItem. 

I hope this blog post gives a good outline of the basic structure and flow of adding Javascript to my Rails app, while also explaining a couple of the finer points that have helped it to run smoothly. Please don't hesitate to reach out if you'd like to chat about the project!

	

