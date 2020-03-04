---
layout: post
title:      "Ruby on Rails AKA Steroids"
date:       2020-03-04 23:45:41 +0000
permalink:  ruby_on_rails_aka_steroids
---


I say Ruby on Steroids because it makes a lot of the manual work normally done to create an app very easy and organized. Using the generators speed up the setup process by a large magnitude. This is another step above using Sinatra. While automating RESTful routes, it's super fast to get a new application up and running.

For my project I created an appointment maker for customers into select stores. The process to create the application was straightfoward and simple using rails. I generated resources for the models I needed and it automatically created the associated files and routes. Knowing the standard process flow for controllers and routes makes the creation of the app smooth. After testing the models, I started building out the controllers and views. 

The most complicated controller was the users/sessions controller. These controllers manage users logging in and out of the application. It had to have the ability of logging someone in from the signup page or from Facebook using omniauth. After that, the focus was mainly on how the application needed to flow and look. Then the beginning of the Build-A-Business-App was born.

Moving forward, I think Ruby on Rails will be a great tool to quickly prototype and test new applications. Especially using a postgres database and heroku. It can be created and available to the public for free in the blink of an eye.
