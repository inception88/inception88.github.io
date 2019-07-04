---
layout: post
title:      "EnterAction Apparel Wishlist: The Sinatra Project"
date:       2019-07-04 19:00:37 +0000
permalink:  enteraction_apparel_wishlist_the_sinatra_project
---


Learning Sinatra and everything leading up to the Sinatra project has been a great experience. This is this first time in the Flatiron course I've felt like I'm working towards making a fully functional website. The concepts will continue to be useful going forward. Let's go through what was taught.

SQL was first in this section. This was very helpful in understanding how databases are structured and how they relate to objects. Basically, the rows in a table relate to unique instances of a class. This leads directly into ORM, Object Relational Mapping, and ActiveRecord. ActiveRecord gives a standard set of functions that allow quick setup of a database and interaction with it. At this point, the goal was to be able to use a database and be able to get the data online. This is where Rack came in.

Rack was interesting because I could see how requests and routes worked on the internet. Using this in combination with ActiveRecord allowed for an interaction between an online site and the database feeling a lot more like a full stack from the frontend to the backend. Then Sinatra came in and I saw the MVC (Model, View, Controller) Architecture to further drive in how a website flows. In a MVC architecture you can go all the way from a user fully embracing a web application because they can interact with the data through all the abstract layers created to the data itself. This is where the Sinatra project comes in.

The EnterAction Apparel wishlist is a culmination of all the lessons above. It allows a user to create a user profile and add products to a wishlist. It's a simple idea that uses a lot of proper planning to lay out and execute. I have models for the products, users and wishlists with different associations and tables in the database. The Sinatra controller allows me to direct the traffic and route users to the proper pages. The views are erb(Embedded Ruby) files, like a ruby/HTML hybrid, that allows easy use of ruby in the page directly. With all of these tools, it's great to be able to create a fully functional webpage from scratch. I'm on the way to becoming a real web developer!

Each of these lessons built on each other to ultimately make understanding an entire web application more simplified. After completing this project I'm excited to see the power of Rails. If it makes these same concepts even easier to implement, I see a lot fo fun times ahead!
