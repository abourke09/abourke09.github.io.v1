---
layout: post
title:      "CLI Project"
date:       2018-04-26 15:28:40 -0400
permalink:  cli_project
---


If you haven’t seen the infographic [“The Emotional Journey of Creating Anything Great”](https://personalexcellence.co/blog/emotional-journey-creating-infographic/) yet, it’s worth a look. Suffice it to say, this project took me through the Dark Swamp of Despair a few times. But let me clarify- it’s not the project’s fault.

Before I even read the CLI Project description in the curriculum, I’d heard people describe their struggles with it. Cue the fear. It didn’t help that the preceding “practice” lab, Tic Tac Toe with AI, put me through the ringer. So before I even clicked on the CLI Project page, I was already paralyzed. If I could give my past self some advice, it would be this:

* Take a deep breath. You can do this (really!) It’s not actually that hard.
* Before you do anything else, read the entire project description page in the curriculum. Then read it again. 
* Pull out your calendar and sign up for every single study group, Q&A session, ect that’s related to the CLI project. 
* Go review the GitHub portion of the curriculum.
* Watch the entire video “CLI Gem Walkthrough” of Avi building a CLI. Don’t try to code anything the first time, just watch. No distractions. Review his code repo on GitHub.
* Read other students’ blog posts on their CLI Projects, take a look at their code repos on GitHub.
* BEFORE you start coding anything, run “curl [your-website-url]” in your terminal (explained further below).
* Once you’ve picked an appropriate website, ask yourself how you’ll organize your file structure for your project. Then, and only then, can you start coding. 
* When you do start coding, feel free to rewatch the CLI Gem Walkthrough video again and reference other students’ examples as you go along.
* For help on your CLI Project, you can schedule up to four sessions with instructional support. More info [here](http://help.learn.co/instructional-support/receiving-course-support/who-can-i-contact-for-help-on-my-portfolio-project ).

As you can see, I believe the biggest challenge of this project has nothing to do with coding. For me at least, it had everything to do with mental preparation and stepping out of my comfort zone for the first time. Regardless, it was an incredibly valuable lesson and I know I’m better off for having learned it.

**Check your website: a note on running “curl [your-website-url]” in your terminal:**
You need to make sure your chosen website is appropriate for this project. Since you’ll be scraping with Nokogiri, the website type should be HTML. If it’s written with Javascript or has anything fancy -like React- incorporated, Nokogiri won’t work. You don’t want to code through half of your project only to get stuck on this small but significant detail. 

A great way to check your website is to run it in terminal with “curl”. So first, open your computer’s terminal. Type “curl” then the url of your chosen website. See my screenshot below for an example. When you press Enter, you should see the website’s code print out the same way you see when using Inspect Element or View Source on the website itself. 

**A note about the legality of scraping:**
Did you know that a lot of websites actively block users from scraping their website? When abused, scraping can really slow down a website. For that reason, there are sometimes features installed that block the IP address of users who attempt to scrape too much. If you’re interested in learning about it, Google around and read up on the subject. At the very least I’d look up your website’s “robots.txt” and learn how to interpret what’s allowed and what’s not on that particular site. 
