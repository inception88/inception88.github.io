---
layout: post
title:      "SPA Profit & Pricing Calculator Using JavaScript and Ruby on Rails API"
date:       2020-06-27 21:04:05 +0000
permalink:  spa_profit_and_pricing_calculator_using_javascript_and_ruby_on_rails_api
---


I created a single page app using Javascript as the frontend and Rails as an API backend. It's a calculator that can add products and expenses that will help you generate prices and determine your profit for a business. If you're starting a new business, it's always great to understand the earning potential it has. And it's more fun to create a web app than just using excel. 

Creating this type of app using AJAX has been a great opportunity to use multiple coding languages in one application. Also, understanding that JSON is simply an object with keys and values has been a nice learning opportunity. A standard, simplified package makes it easy to move data around.

An example is the calculator controller showing how json is passed. When a fetch is made and the return is json from the database, you just need to check the struture to pull any info you need:

```
class CalculatorsController < ApplicationController
    def index
        calculators = Calculator.all
        render json: CalculatorSerializer.new(calculators)
    end
```

This code will return a json object that looks like this:

![](https://drive.google.com/thumbnail?id=1Nb3xFQNx8lMS_nTyZBe2QVWSUSIzFlfF)

The objects that are returned in this instance come from the serializer setup:

```
class CalculatorSerializer
    include FastJsonapi::ObjectSerializer
    attributes :id, :name, :individualGoal, :monthlyGoal
    has_many :products
    has_many :expenses
end
```

This puts all of the attributes needed into one location, making the code more concise in the controller. All of this is the Ruby code for the backend, but it starts from the main javascript file. In this single page app, all the changes are made through JavaScript. All of the forms and buttons have the default action prevented and the page itself updates, but never changes. The fetches use the controller path to interact with the database and return the information in JSON form. All of these actions are used to update the single page.

For instance, adding a product to a calculator will also update the page with the new product:

```
static addProduct(json) {

        if (!("error" in json)) {
                this.removeClass("product-name")
                this.removeClass("cost")
                this.removeClass("commission")
                this.removeClass("netPercentage")
                const product = json
                const table = document.getElementById('products')
                const tr = document.createElement('tr');
                tr.id = `${product['attributes']['id']}`
                this.addRowData(tr, product, 'name')
                this.addRowData(tr, product, 'sales')
                this.addRowData(tr, product, 'cost')
                this.addRowData(tr, product, 'commission')
                this.addRowData(tr, product, 'frequency')
                this.addRowData(tr, product, 'netPercentage')
                this.addRowData(tr, product, 'profit')
                this.addRowData(tr, product, 'price')
                const button = document.createElement('button');
                button.innerText = "Update"
                button.id = `${product['attributes']['id']}`
                button.className = "vertical-center"
                button.addEventListener("click", function() {
                    Product.updateProduct(tr);
                });
                const button2 = document.createElement('button');
                button2.innerText = "Delete"
                button2.id = `${product['attributes']['id']}`
                button2.className = "vertical-center"
                button2.addEventListener("click", function() {
                            Product.deleteProduct(product['attributes']['id']);
                        });
                tr.appendChild(button);
                tr.appendChild(button2);
                table.appendChild(tr);
            }
```

With this code a row is added with the product information:

![](https://drive.google.com/thumbnail?id=1b8EBCPLIopKWL4SLEaBuP6xVW68Erb0h)

Event listeners are added to each button, forcing a JavaScript function to run and make magic happen. For instance we add a delete button every time we add an expense and attach the deleteExpense function to it:

```
const button2 = document.createElement('button');
button2.innerText = "Delete"
button2.id = `${expense['attributes']['id']}`
button2.className = "vertical-center"
button2.addEventListener("click", function() {
    Expense.deleteExpense(expense['attributes']['id']);
});
```

With the interactions between the frontend and backend, this becomes a fully functioning single page application. JavaScript is used to make any updates to the frontend and Ruby on Rails handles the backend. They interact through the use of fetches and JSON. Now that I figured out what money I could potentially make, I just need to get my business plan ready.

Check out the app on Heroku: https://enteraction-calculator.herokuapp.com/

PS: To get this app to work on Heroku, the Ruby on Rails folder structure had to be standard in the root project folder. Creating an additional folder for frontend and backend didn't work. Also, I used the public folder for the index.html page and JS files.
