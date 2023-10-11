# Using Solr 9.3 as a service with Rails application
Couldn't find recent documentation on the internet so posting here. Hope it helps someone

# Prerequisite for this example -
-	Ubuntu 22.04 installed
-	Java 11 installed
-	MySQL 8.0 installed with database configured
-	Solr 9.3 installed - https://solr.apache.org/guide/solr/latest/deployment-guide/installing-solr.html

# Start Solr 
````
bin/solr start
bin/solr create -c new_core
````
login to http://localhost:8983/solr/#/
confirm new core is available in the Core Admin section

# Configure Solr with Rails app
## Run as development
add gems to Gemfile:

```
gem 'sunspot_rails'
gem ‘sunspot_solr’
```
Install gems:
````
bundle install
````
Generate /config/sunspot.yml file:
```
rails g sunspot_rails:install
```
Don’t need to modify as solr is already running on localhost:8983

Although we have solr running as a service we’ll still need to run the following commands to generate the /solr directory
````
bundle exec rake sunspot:solr:start
bundle exec rake sunspot:solr:stop
````
## [Examples to setup searchable models](https://github.com/sunspot/sunspot)

# Reindex
````
bundle exec rake sunspot:solr:reindex RAILS_ENV=development
````


