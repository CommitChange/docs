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

This is a JSON API gateway using Ruby and Sinatra that interfaces with our Postgresql database. We are actively moving our database business logic into this application (or into other microservices below). It uses cross-site authentications with JWT tokens and can serve any web or mobile app.

* Repo: https://github.com/CommitChange/api
* Location: https://api.commitchange.com
* Stack: Ruby, Sinatra, and Qx
* Host: Heroku/Amazon

The API uses a GraphQL/Postgrest inspired generalized endpoint system with less nesting. It uses a Ruby module structure to generate Postgresql queries for different endpoints and has the ability to run many SQL queries in parallel for one request.

### API Documentation and User Interface

Automatically generated documentation for every API endpoint. These docs get generated dynamically by the frontend making OPTIONS requests to the API, discovering all its endpoints, and formatting the JSON documentation from those requests. You can login and see the endpoints available for your account type (by default it shows only public endpoints).

The documentation site also has the ability to login and construct actual API requests using a GUI. This is still experimental and may prove very useful for support and admin.

* Repo: https://github.com/CommitChange/commitchange.github.io
* Location: http://docs.commitchange.com
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

This is a work-in-progress Python application using Keras to train machine learning models using large CSV datasets from our API.

* Repo: https://github.com/CommitChange/ml
* Stack: Python, Flask, Keras
* Host: Heroku

### Reporting Database (Metabase)

A business intelligence reporting app for showing platform activity, sales performance, creating custom exports for clients, etc etc.

* Repo: https://github.com/CommitChange/metabase
* Location: https://commitchange-metabase.herokuapp.com
* Stack: Metabase, Postgresql, Clojure
* Host: Heroku

### File Upload Server

This is an Amazon S3 file upload microservice with image resizing capabilities that the API gateway and other services can use.

* Repo: https://github.com/CommitChange/file-upload-server
* Location: https://uploads.commitchange.com
* Stack: Ruby and Sinatra
* Host: Heroku

### Webhooks Server

This is a microservice (and client to the API) that listens for webhook events from services like Stripe and updates the database correspondingly.

* Repo: https://github.com/CommitChange/webhook-listeners
* Location: https://webhooks.commitchange.com
* Stack: Ruby and Sinatra
* Host: Heroku

### Commons.css

Our base CSS files for our CommitChange-branded web components. This can be installed with npm.

* Repo: https://github.com/CommitChange/commons.css
* Stack: postcss, postcss-import, precss, normalize

# Future Expansion

* Use Ruby YARD and Javascript ESDoc to add in-code documentation throughout the entire platform.
* Increase collection of Ruby Gems and NPM modules by extracting discrete functionality out of the apps.
* Migrate all the commitchange.com frontend to unit-tested, npm-hosted Flimflam components and Postcss modules
* Migrate commitchange.com to be purely a frontend client to the API gateway.
* Create a payment Audits server that is an API client and has crons for checking the database on the data, performing regularly scheduled audits, and emailing and results
* Add Websocket based real-time messaging support for the API for things like campaign activity and metrics

# Support and Maintenance

We keep track of dev support tickets here: https://github.com/commitchange/tix/issues. We spend on average 10 dev-hours per week on support.
