# LinuxDeploy
Deploying final project on Linux

Public IP 13.127.247.243

Application URL http://info.adventureguild.in

Allowed ADmin account to Udacity reviewer : grader

SSH keys shared separately to reviewer

root login disabled

SSH port 2200

DB used postgresql

JSON working

http://info.adventureguild.in/list/JSON

FIRST OBJECTIVE IS TO UPDATE THE SERVER 

run the command sudo apt-get update to update the server.

Once the update are over run the command sudo apt-get upgrade to upgrade the server.

The python edition is already available, make sure it is upto date and below mentioned python modules.

/MODULE REQUIREMENT FOR PYTHON TO RUN THIS APPLICATION/ 

Flask

SQLAlchemy

Flask-SQLAlchemy

Flask-Migrate

Flask-Login

requests-oauthlib

psycopg2

httplib2

oauth2client

sqlalchemy_utils

INSTALL APACHE by running the command sudo apt-get install apache2

INSTALL DATABASE sudo apt-get install postgresql

NETWORK MODIFICATION
AWS LIGHTSAIL IN ACCORDANCE WITH BELOW RULES

sudo ufw allow 2200/tcp

sudo ufw allow www

sudo ufw allow 123/udp

sudo ufw deny 22

sudo ufw default deny incoming

sudo ufw default allow outgoing

sudo ufw enable

sudo ufw status

create wsgi file with the detail

#!/usr/bin/python

import sys

import logging

logging.basicConfig(stream=sys.stderr)

sys.path.insert(0,"/var/www/FlaskApp/")

from FlaskApp import app as application

#now create a conf file and update it with below details 

<VirtualHost *:80>
                ServerName info.adventureguild.in
                ServerAdmin someone@important.com
                WSGIScriptReloading On
                WSGIDaemonProcess FlaskApp user=ubuntu threads=5
                WSGIScriptAlias / /var/www/FlaskApp/flaskapp.wsgi
                <Directory /var/www/FlaskApp/FlaskApp/>
                        Require all granted
                </Directory>
                Alias /static /var/www/FlaskApp/FlaskApp/static
                <Directory /var/www/FlaskApp/FlaskApp/static/>
                        Require all granted
                </Directory>
                Alias /templates /var/www/FlaskApp/FlaskApp/templates
                <Directory /var/www/FlaskApp/FlaskApp/templates/>
                        Require all granted
                </Directory>
                ErrorLog ${APACHE_LOG_DIR}/error.log
                LogLevel warn
                CustomLog ${APACHE_LOG_DIR}/access.log combined
</VirtualHost>

using SCPcopy copy the project from local drive to server in location var/www/FlaskApp/FlaskApp

Create DB 

sudo su - postgres

CREATE USER catalog WITH PASSWORD 'pass';

\du

CREATE DATABASE unitdata;

\l


update createdb and generatedata and __init__.py code with postgresdb instead of SQLite .

engine = create_engine('postgresql://catalog:pass@localhost/unitdata',echo=True)

resources used

udacity forum

youtube on databases

stack overflow

digitalocean 
