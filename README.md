# linux_server_config
Linux server set up for the [Catalog App](https://github.com/nicholsont/catalog_app/blob/postgres/README.md)

## ssh 
Connects to the server via ssh.
```
ssh grader@54.191.58.90 -p 2200
```

## Application URL
Access Catalog App with ip address
```
http://54.191.58.90
```

## Installation
1. Software
  * Apache2
  ```
  sudo apt-get install apache2
  ```
  * libapach2mod_w
  ```
  sudo apt-get install libapache2-mod-wsgi
  ```
  * PosgreSQL 9.5
  ```
  sudo apt-get install postgresql
  ```
  * git
  ```
  sudo apt-get install git
  ```
  * Python-pip
  ```
  sudo apt-get install python-pip
  ```
2. Python Dependencies
  * Flask
  ```
  sudo pip install flask  
  ```
  * Psycopg2
  ```
  sudo pip install psycopg2 
  ```  
  * SQLAlchemy
  ```
  sudo pip install SQLAlchemy    
  ```  
  * Requests
  ```
  sudo pip install requests
  ```  
  * Oauth2Client (Google Oauth)
  ```
  sudo pip install oauth2client 
  ```

## Configurations
1. Apache 2
  - Edit 000-default.conf file
    *Edit the document root containing both the app and wsgi scripts
      ```
        DocumentRoot /var/www/catalog
      ```
    *Set the root directory of the app and its access configurations
      ```
        <Directory /var/www/catalog/app>
              Options Indexes FollowSymLinks MultiViews
              AllowOverride None
              Order allow,deny
              Allow from all
        </Directory>
      ```
    *Set the WSGI script alias and root directory
      ```
        WSGIScriptAlias / /var/www/catalog/wsgi-scripts/myapp.wsgi

        <Directory /var/www/catalog/wsgi-scripts>
              Order deny,allow
              Allow from all
        </Directory>
      ```
2. PostgreSQL 9.5
  - Setup postgres user password
    * Login to postgres
      ```
      sudo -u postgres psql postgres
      ```
    * Create a password
      ```
      \password
      ```
  - Edit pg_hba.conf
    * Change domain socket connection from peer to md5
      ```
      # Database administrative login by Unix domain socket
      local       all         postgres                      md5
      ```
## References
The sites below were referenced during the configuration process.
  - [Running a Flask application under the Apache WSGI module](https://www.jakowicz.com/flask-apache-wsgi/)
  - [Quick configuration guide for mod_wsgi](https://code.google.com/archive/p/modwsgi/wikis/QuickConfigurationGuide.wiki)
  - [Deploying Flask Apps with Apache and Mod WSGI](https://beagle.whoi.edu/redmine/projects/ibt/wiki/Deploying_Flask_Apps_with_Apache_and_Mod_WSGI?version=3)
  - [How to deploy Flask applications to Apache webserver](http://csparpa.github.io/blog/2013/03/how-to-deploy-flask-applications-to-apache-webserver.html)
  - [Connecting to PostgreSQL on Linux for the first time](http://suite.opengeo.org/docs/latest/dataadmin/pgGettingStarted/firstconnect.html)
