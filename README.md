# Event Log File Browser

A Salesforce connected web app to access and download Event Log Files. **Access it on [Heroku](https://salesforce-elf.herokuapp.com/).**

## Overview

[Salesforce event log file](https://www.salesforce.com/us/developer/docs/api_rest/Content/using_resources_event_log_files.htm) is a file-based API to get your Salesforce organization's application log data. These files provide visibility into your org for security auditing, application performance, and feature adoption. 

Event log file browser is a Salesforce connected app built with Ruby on Rails to help you access and download event log files. The downloads are streamed to the web client via the Rails application using Rail's `ActionController::Streaming`.

## Hosting your own instance of Salesforce Event Log File Browser

### Heroku
[![Deploy](https://www.herokucdn.com/deploy/button.png)](https://heroku.com/deploy)

### Other platforms
Follow these steps if you wish to host your own instance of the application on any Rails hosting platform.

#### Create Salesforce consumer key and secret
This step can be performed from any Salesforce organization.

1. Navigate to **Setup > Create > Apps > Connected Apps > New**
2. In the **New Connected App** page, check **Enable OAuth Settings**.
3. Enter the callback URL. For localhost, use `http://localhost:3000/auth/salesforce/callback`. If it's hosted, use `https://<your domain>/auth/salesforce/callback`. If you do not use SSL, you must set `config.forcessl = false` in **config/environments/production.rb**
4. Add **Access and manage your data (api)** to the **Selected OAuth Scopes**.
5. Fill out the remaining required fields and click **Save**.
6. Once you save, you'll be taken to a page that has the consumer key and consumer secret.
7. Repeat steps 1-6 for sandbox instance with a slight change in step 3 -- replace `.../auth/salesforce/callback` with `.../auth/salesforcesandbox/callback`
8. Note your consumer key and secret and for both production and sandbox instances.

#### Configure and start Rails or Docker
Configure the following environment variables.

1. `SALESFORCE_ELF_CONSUMER_KEY`: (required) Salesforce consumer key for production from previous section.
2. `SALESFORCE_ELF_CONSUMER_SECRET`: (required) Salesforce consumer secret for production from previous section.
3. `SALESFORCE_ELF_SANDBOX_CONSUMER_KEY`: (required) Salesforce consumer key for sandbox from previous section.
4. `SALESFORCE_ELF_SANDBOX_CONSUMER_SECRET`: (required) Salesforce consumer secret for sandbox from previous section.
5. `SECRET_KEY_BASE`: (required) Secret key for encryption that you can generate using `rake secret`. Rotate the keys periodically.
6. `ELF_MAX_DOWNLOAD_FILE_SIZE_IN_BYTES`: (optional) The maximum size of file allowed via streaming download. Default is 5_000_000 (~5MB).
7. `ELF_GOOGLE_ANALYTICS_TRACKING_ID`: (optional) For Google Analytics tracking.

If using Rails, once the environment variables are setup, you can start the application using `rails server` or `foreman start`.

If using Docker, the environment variables can be added to a `.env` file or passed through to the container and started with `docker-compose up`

If you would like to load the variables from a file at runtime rather than the environment, it is possible to store them all in a single YAML file and set an `ENV_YAML` environment variable. This is sometimes prefered if secrets would be stored apart from deployment configuration or if one does not want secrets stored within the images themselves.

## Issues
Report bugs and issues [here](https://github.com/abisek/salesforce-elf-browser/issues).

## Contributors
(Listed in no particular order)

* [Abhishek Sreenivasa](https://github.com/abisek) - developer and maintainer
* [Adam Torman](https://github.com/atorman) - QA and product management
* Soumen Bandyopadhyay - QA
* Ivan Weiss - QA
* Justine Heritage - documentation
* Aakash Pradeep - QA
