Getting Started with Docker for Development
===========================

** THIS DOCKER CONFIGURATION IS INTENDED FOR DEVLOPMENT & DEVELOPMENT PURPOSES ONLY**

The main difference between the Dev and Test dockers is that the Dev has NPM, Node, composer, and Cypress installed and running inside the docker.


Development
-------------

These are the steps needed to develop ChurchCRM with Docker

## Requirements

* Docker
* Docker Compose
* GIT
* Node and NPM

## Steps

1. Clone ChurchCRM Repo `git clone git@github.com:ChurchCRM/CRM.git`
2. `cd` into the project directory
2. build docker `npm run docker-dev-build`
3. start the containers `npm run docker-dev-start` . **Note:** Containers are started in the background
4. ssh into the web container `npm run docker-dev-login-web`
5. cd into src code `cd /home/ChurchCRM`
6. build church crm web and php code `npm run deploy`
7. make the application log folder writable: `chmod a+rwx src/logs`
10. stop docker `npm run docker-dev-stop`. **Note:** Run this command from your host system
11. To view the live logs run `npm run docker-dev-logs`. **Note:** Run this command from your host system

### Dev containers
   - database : Mariadb server
      - exposes port **3306** by default. You can change this port by updating *DEV_DATABASE_PORT* in the file `docker/.env`.

      Internally, the port is always **3306**
   - webserver : The web server and container that contains all of the application's code
      - exposes port **80** by default. You can change this port by updating *DEV_WEBSERVER_PORT* in the file `docker/.env`.
      
         Internally, the port is always **80**
   - adminer : Simple web application to access the database server graphically
      - exposes port **8088** by default. You can change this port by updating *DEV_ADMINER_PORT* in the file `docker/.env`

         Internally, the port is always **8080**
      - default credentials
         - username: `churchcrm`
         - password: `changeme`
         - default database: `churchcrm`
         - root user password: `changeme`

   - mailserver : SMTP testing server. A *fake* email inbox
      - exposes port **1025** and **8025**. These ports can be changed
        by updating *DEV_MAILSERVER_PORT* and *DEV_MAILSERVER_GUI_PORT* respectively.
        Port **8025** is the application's UI port.

Testing
-----------------

if you are developing on your local dev system and testing via docker, use the following:

## Requirements

* Docker
* Docker Compose
* GIT
* node / npm

1. Clone ChurchCRM Repo `git clone git@github.com:ChurchCRM/CRM.git`
2. build code `npm run deploy`
3. build docker `npm run docker-test-build`
4. run docker `npm run docker-test-start`
5. test code `npm run docker-ci`
10. stop docker `npm run docker-test-stop`
