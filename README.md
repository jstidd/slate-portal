[![Build Status](https://travis-ci.org/globus/globus-sample-data-portal.svg?branch=master)](https://travis-ci.org/globus/globus-sample-data-portal)

# Modern Research Data Portal
Simple web app framework demonstrating how to build a data portal using
the Globus [platform](https://www.globus.org/platform).

## Overview
This repository contains two separate server applications. The first, the "Portal," is an example "research portal"
that demonstrates how to authenticate users with Globus [Auth](https://docs.globus.org/api/auth/), how to make requests against the Globus [Transfer API](https://docs.globus.org/api/transfer/), and how to interact with an HTTPS-enabled Globus Endpoint. All of the Portal code can be found in the `portal/` directory.

The second application, the "Service," is an example "resource server" that demonstrates how a research portal can offload tasks to a separate service that has the capability to perform tasks on behalf of users. All of the Service code can be found in the `service/` directory.

## Getting Started
#### Set up your environment.
* [OS X](#os-x)
* [Linux](#linux-ubuntu)
* [Windows](#windows)
* [Amazon EC2](#amazon-ec2)

#### Create your own App registration for use in the Portal. 
* Visit the [Globus Developer Pages](https://developers.globus.org) to register an App.
* If this is your first time visiting the Developer Pages you'll be asked to create a Project. A Project is a way to group Apps together.
* When registering the App you'll be asked for some information, including the redirect URL and any scopes you will be requesting.
    * Redirect URL: `https://localhost:5000/authcallback` (note: if using EC2 `localhost` should be replaced with the IP address of your instance).
    * Scopes: `urn:globus:auth:scope:transfer.api.globus.org:all`, `openid`, `profile`, `email`
* After creating your App the client id and secret can be copied into this project in the following two places:
    * `portal/portal.conf` in the `PORTAL_CLIENT_ID` and `PORTAL_CLIENT_SECRET` properties.
    * `service/service.conf` where the `PORTAL_CLIENT_ID` is used to validate the access token that the Portal sends to the Service.

### OS X

##### Environment Setup

* `sudo easy_install pip`
* `sudo pip install virtualenv`
* `git clone https://github.com/globus/globus-sample-data-portal`
* `cd globus-sample-data-portal`
* `virtualenv venv`
* `source venv/bin/activate`
* `pip install -r requirements.txt`

##### Running the Portal App

* `./run_portal.py`
* point your browser to `https://localhost:5000`

##### Running the Service App

* `./run_service.py`
* API is located at `https://localhost:5100/api`

### Linux (Ubuntu)

##### Environment Setup

* `sudo apt-get update`
* `sudo apt-get install python-pip python-dev gcc`
* `sudo pip install virtualenv`
* `sudo apt-get install git`
* `git clone https://github.com/globus/globus-sample-data-portal`
* `cd globus-sample-data-portal`
* `virtualenv venv`
* `source venv/bin/activate`
* `pip install -r requirements.txt`

##### Running the Portal App

* `./run_portal.py`
* point your browser to `https://localhost:5000`

##### Running the Service App

* `./run_service.py`
* API is located at `https://localhost:5100/api`

### Windows

##### Environment Setup

* Install Python (<https://www.python.org/downloads/windows/>)
* `pip install virtualenv`
* Install git (<https://git-scm.com/downloads>)
* `git clone https://github.com/globus/globus-sample-data-portal`
* `cd globus-sample-data-portal`
* `virtualenv venv`
* `venv\Scripts\activate`
* `pip install -r requirements.txt`

##### Running the Portal App

* `python run_portal.py`
* point your browser to `https://localhost:5000`

##### Running the Service App

* `python run_service.py`
* API is located at `https://localhost:5100/api`

### Amazon EC2

##### Environment Setup

* `git clone https://github.com/globus/globus-sample-data-portal`
* `cd globus-sample-data-portal`
* `virtualenv venv`
* `source venv/bin/activate`
* `pip install -r requirements.txt`
* `sed -i 's/localhost/0.0.0.0/' run_portal.py`
* `sed -i '4,//s/localhost/YOUR_IP/' portal/portal.conf`
* `echo "SESSION_COOKIE_DOMAIN = 'YOUR_IP'" >> portal/portal.conf`

##### Running the Portal App

* `./run_portal.py`
* point your web browser to `https://YOUR_IP:5000/`

##### Running the Service App

* `./run_service.py`
* API is located at `https://localhost:5100/api`
