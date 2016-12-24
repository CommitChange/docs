# CommitChange Platform Overview

## Web Services, Applications, and Libraries

### CommitChange.com  

This application comprises the main CommitChange product for nonprofits, all of the frontend of commitchange.com, and much of our backend business logic with Postgresql and Ruby.

* Repo: https://github.com/CommitChange/commitchange.com
* Location: https://commitchange.com
* Stack: Rails 3.2
* Frontend: http://flimflamjs.github.io/
* Backend: Postgresql and [Qx](https://github.com/jayrbolton/ruby-qx)
* Host: Heroku/Amazon

This repo is actively maintained and iterated. We have no plans to upgrade to Rails 4 or 5 and are instead transitioning into a more modular, microservices-oriented approach by moving the business logic into separate applications. We are migrating the Rails asset pipeline into a Node build process using Browserify and PostCSS.

### API

This is a JSON API gateway using Ruby and Sinatra that interfaces with our Postgresql database. We are actively moving our database business logic into this application (or into other microservices below).

* Repo: https://github.com/CommitChange/api
* Locatino: https://api.commitchange.com
* Stack: Ruby, Sinatra, and Qx
* Host: Heroku/Amazon

The API uses a GraphQL/Postgrest inspired generalized endpoint system with less nesting.

### API Admin Interface

This is an experimental, generalized UI for directly interacting with the API as an authenticated user (eg for doing support or admin).

* Repo: https://github.com/CommitChange/api-gui
* Location: https://api-gui.commitchange.com
* Stack: Frontend only (with [Flimflam](http://flimflamjs.github.io/))
* Host: Heroku

### API Documentation

Automatically generated documentation for every API endpoint. These docs get generated dynamically by the frontend making OPTIONS requests to the API, discovering all its endpoints, and formatting the JSON documentation from those requests. You can login and see the endpoints available for your account type (by default it shows only public endpoints).

* Repo: https://github.com/CommitChange/commitchange.github.io
* Location: https://docs.commitchange.com
* Stack: Sinatra and [Flimflam](http://flimflamjs.github.io/)
* Host: Heroku

### API Ruby Gem

This is a Ruby Gem wrapper around the API for easily using the API endpoints from the backends of other Ruby applications.

* Repo: https://github.com/CommitChange/api-ruby-gem
* Stack: Ruby

### Javascript SDK

This is an embedable javascript file for third-party websites (such as Wordpress and Squarespace) that allows people to insert and control CommitChange fundraising widgets like the donate button, campaign cards, and supporter forms.

* Repo: https://github.com/CommitChange/sdk
* Stack: Plain JS

### Machine Learning App 

This is a work-in-progress Python application using Keras to train machine learning models using CSV results from our API.

* Repo: https://github.com/CommitChange/ml
* Location: https://ml.commitchange.com
* Stack: Python, Flask, Keras
* Host: Heroku

### Reporting Database (Metabase)

A business intelligence reporting app for showing platform activity, sales performance, creating custom exports for clients, etc etc.

Repo: https://github.com/CommitChange/metabase
location: https://commitchange-metabase.herokuapp.com
Stack: Metabase (Clojure)
Host: Heroku

### File Upload Server

This is an Amazon S3 file upload microservice with image resizing capabilities that the API gateway and other services can use.

### Webhooks Server

This is a microservice (and client to the API) that listens for webhook events from services like Stripe and updates the database correspondingly.

* Repo: https://github.com/CommitChange/webhook-listeners
* Location: https://webhooks.commitchange.com
* Host: Heroku

### Commons.css

Our base CSS files for our CommitChange-branded web components. This can be installed with npm.

Repo: https://github.com/CommitChange/commons.css
Stack: postcss, postcss-import, precss, normalize

# Future Expansion

* Create a payment Audits server that is an API client and has crons for checking the database on the data, performing regularly scheduled audits, and emailing and results
* Increase compendium of Ruby Gems (eg 
