---
layout: post
title:      "React on Rails: Launching a React frontend and Rails backend app on Heroku"
date:       2020-12-22 00:03:47 +0000
permalink:  react_on_rails_launching_a_react_frontend_and_rails_backend_app_on_heroku
---


For my final Flatiron School Project I decided to build something that would actually be helpful for my future entrepreneurial endeavors: [Trademarkfollower.com](http://www.trademarkfollower.com) This web app pulls data from the USPTO's TSDR database and let's you store all the trademarks and links to them in one location. This gave me an opportunity to use React, Ruby on Rails, and pull data from a real external API. Let's talk about the challenges and successes of building a web application this way.

Step one for me was to test out the API calls and see what information I could get from the TSDR database. After getting my API key, I used [postman](http://www.postman.com) to determine the best way to use the API. After successfully pulling the data I needed, I created the basic front end app and rails api backend app to test fetch calls directly. When I had both apps setup, I tested out the call to the TSDR API and saw a term I hadn't seen before: CORS - Cross-Origin Resource Sharing.

![CORS Policy](https://drive.google.com/uc?id=118YcM97MM0PoSULuwQEGZqlhZ-wPvWRW)

CORS becomes a problem with browsers blocking responses from anything outside of the original domain. If you're working in a development environment, localhost is a separate domain from any API you can call. Checkout this image from Moizilla for a better understanding:

![Web Requests](https://mdn.mozillademos.org/files/14295/CORS_principle.png)

After doing A LOT of research, there are multiple ways of preventing the CORS issue. One is to allow all requests from the API. Or you can specify which domains are allowed access outside of the origin. I did this with the trademark-follower-api Rails app and updated the cors.rb file to allow access from localhost and trademarkfollower.com. The issue comes in when you need access to an external API. You can't update their server to allow access from your application. The solution I've come upon becomes creating a proxy server that basically is the in between communication and talks directly from a server instead of the browser preventing the CORS issue. A solution that was a little simpler than creating a proxy was using cors anywhere. https://cors-anywhere.herokuapp.com/ When you use this link in front of your link address, it handles the request/responses for you. For example, this is what I used to do searches: 

```
//TrademarkSearch.js
    fetch(`https://cors-anywhere.herokuapp.com/https://tsdrapi.uspto.gov/ts/cd/casestatus/sn${sn}/info`, { headers: {"USPTO-API-KEY": API_KEY}}

```

I don't like this as a permanent solution, but this works for now. After getting beyond the CORS issue, I started building out the React components for the frontend. I started with the trademark search capability, then moved on to the navbar. I used the antd library to create a navbar. I used react-router-dom to setup routes and links between the main pages. The challenge here was to only allow certain routes when someone is logged in or not. Conditionals work a little differently in JSX. I used the method below to have links only show up during certain times.

```
          {this.props.authenticated && <Menu.Item ><Link to="/logout">
          Logout
          </Link></Menu.Item>}
```

Then I created the actual user signup/login/logout. This app uses JWT and bcrypt in Ruby to encrypt the user's info. I decided to use Redux to store the current user info. After setting up the user signup and login process locally, I decided to start using the app on Heroku.

Setting up an app on Heroku is really easy. I use github to automatically deploy the master or main branch of the app. This way anytime I make an update on the master/main it will automatically update the live web app. For the backend I connect a free Heroku postgres database. After adding the database all you have to do is add 2 lines  for the production database and then rake db:migrate in the Heroku console:

![Auto Deploy](https://drive.google.com/uc?id=1MrXKWmG0UV7crWk9rk4uCxahj2OZ383d)

![Heroku Database](https://drive.google.com/uc?id=1Fzb7mqki0Klhu7DiAoImitnOUtImWRDh)

```
//database.yml
production:
  url: <%= ENV['DATABASE_URL'] %>
```

Heroku will automatically add the variables needed for the database.

![Database Variables](https://drive.google.com/uc?id=1wxlGl-4jlNCt72w86mw9J2zgd2upnHE9)

Rune the rake command and you should be good to go!

```
//heroku console
rake db:migrate
```

For the frontend I had some issues until I changed the scripts in package.json to match below:

```
  "scripts": {
    "dev": "react-scripts start",
    "start": "serve -s build",
    "build": "react-scripts build",
    "test": "react-scripts test --env=jsdom",
    "eject": "react-scripts eject",
    "heroku-postbuild": "npm run build"
  },
```

After this my front end app starting working properly. The biggest change is that you have to start the development server by running: `npm run dev` instead of `npm start`. Also, if you want to use a custom domain all you have to do is purchase the domain name (I use [namecheap](http://www.namecheap.com)) and put that info into Heroku. It asks you for your credit card info, but it doesn't charge you anything until usage of the app goes beyond a certain point.

![Custom Domain](https://drive.google.com/uc?id=1XoQ3iYJxCQQw-0XjFOzkW_i6l_A6zYMX)

In the end, this was a great experience to get a fully functioning web app with a React frontend and a separate Ruby on Rails backend. I'm excited that I can create a complete full stack application from scratch and set it up with a custom domain. I can't wait for the next project I work on and growing Ben Jones Codes with my new skills.
