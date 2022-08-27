---
title: Gunicorn + daphne + nginx Django project deploy
keywords: Gunicorn Bangla Tutorials, daphne expression bangla, nginx bangla, Gunicorn + daphne + nginx , Bangla Django deploy, Blog Bangla, Monad wizard
last_updated: august 27, 2022
# tags: [getting_started]
summary: 'Here I try to complete all Basic Gunicorn + daphne + nginx Django project deploy Topic with short note. '
sidebar: mydoc_sidebar
permalink: gunicorn,daphne,nginx_django.html
folder: mydoc
---

## 1st of all install dependency

    sudo apt update
    sudo apt install python3-pip python3-dev libpq-dev postgresql postgresql-contrib nginx curl

#### Creating the PostgreSQL Database and User

Log into an interactive Postgres session by typing:

```
    sudo -u postgres psql
```

#### First, create a database for your project

```
    CREATE DATABASE myproject;
```

#### Next, create a database user for our project. Make sure to select a secure password

```
    CREATE USER myprojectuser WITH PASSWORD 'password';
```

We are setting the default encoding to UTF-8, which Django expects. We are also setting the default transaction isolation scheme to “read committed”, which blocks reads from uncommitted transactions. Lastly, we are setting the timezone. By default, our Django projects will be set to use UTC. These are all recommendations from the Django project itself:

```
    ALTER ROLE myprojectuser SET client_encoding TO 'utf8';
    ALTER ROLE myprojectuser SET default_transaction_isolation TO 'read committed';
    ALTER ROLE myprojectuser SET timezone TO 'UTC';
```

Now, we can give our new user access to administer our new database:

```
    GRANT ALL PRIVILEGES ON DATABASE myproject TO myprojectuser;
```

When you are finished, exit out of the PostgreSQL prompt by typing:

```
    \q
```

## Creating a Python Virtual Environment for your Project

To do this, we first need access to the virtualenv command. We can install this with pip.If you are using Python 3, upgrade pip and install the package by typing:

```
    sudo -H pip3 install --upgrade pip
    sudo -H pip3 install virtualenv
```

With virtualenv installed, we can start forming our project. Create and move into a directory where we can keep our project files:

```
    mkdir ~/myprojectdir
    cd ~/myprojectdir
```

Within the project directory, create a Python virtual environment by typing:

```
    virtualenv myprojectenv
```

With virtualenv installed, we can start forming our project. Create and move into a directory where we can keep our project files:

```
    source myprojectenv/bin/activate
```

With your virtual environment active, install Django, Gunicorn, and the psycopg2 PostgreSQL adaptor with the local instance of pip:

```
    pip install django gunicorn psycopg2-binary
```

#### Clone and Configuring a New Django Project

Clone your existiong Django project from Git :

```
    Git clone HTTP_URL
```

Open the settings file in your text editor:

```
    nano ~/myprojectdir/myproject/settings.py
```

Start by locating the ALLOWED_HOSTS directive. This defines a list of the server’s addresses or domain names may be used to connect to the Django instance. Any incoming requests with a Host header that is not in this list will raise an exception. Django requires that you set this to prevent a certain class of security vulnerability.

```
    ALLOWED_HOSTS = ['your_server_domain_or_IP', 'second_domain_or_IP', . . ., 'localhost']
```

#### Change the settings with your PostgreSQL database information.You can leave the PORT setting as an empty string

```
    DATABASES = {
        'default': {
            'ENGINE': 'django.db.backends.postgresql_psycopg2',
            'NAME': 'myproject',
            'USER': 'myprojectuser',
            'PASSWORD': 'password',
            'HOST': 'localhost',
            'PORT': '',
        }
    }
```

Next, move down to the bottom of the file and add a setting indicating where the static files should be placed. This is necessary so that Nginx can handle requests for these items. The following line tells Django to place them in a directory called static in the base project directory:

```
    . . .

    STATIC_URL = '/static/'
    import os
    STATIC_ROOT = os.path.join(BASE_DIR, 'static/')
```

Save and close the file when you are finished.

Completing Initial Project Setup
Now, we can migrate the initial database schema to our PostgreSQL database using the management script:

```
    ~/myprojectdir/manage.py makemigrations
    ~/myprojectdir/manage.py migrate
```

Create an administrative user for the project by typing:

```
    ~/myprojectdir/manage.py createsuperuser
```

You will have to select a username, provide an email address, and choose and confirm a password.
We can collect all of the static content into the directory location we configured by typing:

```
    ~/myprojectdir/manage.py collectstatic
```

You will have to confirm the operation. The static files will then be placed in a directory called static within your project directory.

Create an exception for port 8000 by typing:

```
    sudo ufw allow 8000
```

Finally, you can test our your project by starting up the Django development server with this command:

```
    ~/myprojectdir/manage.py runserver 0.0.0.0:8000
```

In your web browser, visit your server’s domain name or IP address followed by :8000:

`<http://server_domain_or_IP:8000>`

When you are finished exploring, hit CTRL-C in the terminal window to shut down the development server.

### Testing Gunicorn’s Ability to Serve the Project

The last thing we want to do before leaving our virtual environment is test Gunicorn to make sure that it can serve the application. We can do this by entering our project directory and using gunicorn to load the project’s WSGI module:

```
    cd ~/myprojectdir
```

```
    gunicorn --bind 0.0.0.0:8000 myproject.wsgi
```

When you are finished testing, hit `CTRL-C` in the terminal window to stop Gunicorn.

#### Creating systemd Socket and Service Files for Gunicorn

The Gunicorn socket will be created at boot and will listen for connections. When a connection occurs, systemd will automatically start the Gunicorn process to handle the connection.

## Gunicorn

Start by creating and opening a systemd socket file for Gunicorn with sudo privileges:

```
    sudo nano /etc/systemd/system/myprojectgunicorn.socket
```

Inside, we will create a `[Unit]` section to describe the socket, a `[Socket]` section to define the socket location, and an `[Install]` section to make sure the socket is created at the right time:

```
    [Unit]
    Description=gunicorn socket

    [Socket]
    ListenStream=/run/myprojectgunicorn.sock

    [Install]
    WantedBy=sockets.target
```

Save and close the file when you are finished.

Next, create and open a systemd service file for Gunicorn with sudo privileges in your text editor. The service filename should match the socket filename with the exception of the extension:

```
    sudo nano /etc/systemd/system/myprojectgunicorn.service
```

Start with the `[Unit]` section, which is used to specify metadata and dependencies. We’ll put a description of our service here and tell the init system to only start this after the networking target has been reached. Because our service relies on the socket from the socket file, we need to include a Requires directive to indicate that relationship:

```
    [Unit]
    Description=gunicorn daemon
    Requires=myprojectgunicorn.socket
    After=network.target
```

Next, we’ll open up the `[Service]` section. We’ll specify the user and group that we want to process to run under. We will give our regular user account ownership of the process since it owns all of the relevant files. We’ll give group ownership to the www-data group so that Nginx can communicate easily with Gunicorn.

We’ll then map out the working directory and specify the command to use to start the service. In this case, we’ll have to specify the full path to the Gunicorn executable, which is installed within our virtual environment. We will bind the process to the Unix socket we created within the /run directory so that the process can communicate with Nginx. We log all data to standard output so that the journald process can collect the Gunicorn logs. We can also specify any optional Gunicorn tweaks here. For example, we specified 3 worker processes in this case:

```
    [Unit]
    Description=gunicorn daemon
    Requires=myprojectgunicorn.socket
    After=network.target

    [Service]
    User=serverUsername
    Group=www-data
    WorkingDirectory=/home/project/myprojectdir
    ExecStart=/home/project/myprojectdir/myprojectenv/bin/gunicorn \
    --access-logfile - \
    --workers 3 \
    --bind unix:/run/gunicorn.sock \
    myproject.wsgi:application
```

Finally, we’ll add an `[Install]` section. This will tell systemd what to link this service to if we enable it to start at boot. We want this service to start when the regular multi-user system is up and running:

```
    [Unit]
    Description=gunicorn daemon
    Requires=myprojectgunicorn.socket
    After=network.target

    [Service]
    User=sammy
    Group=www-data
    WorkingDirectory=/home/project/myprojectdir
    ExecStart=/home/project/myprojectdir/myprojectenv/bin/gunicorn \
    --access-logfile - \
    --workers 3 \
    --bind unix:/run/gunicorn.sock \
    myproject.wsgi:application

    [Install]
    WantedBy=multi-user.target
```

#### We can add daphne configuration on gunicorn service

Daphne can bind with a new port and replace ExecStart part from wsgi to asgi file. Then our full django project can execute with asgi configuration instant of wsgi.

For that we have to replace previouse ExecStart and add daphne path which install in invironment with an unique port which is allowed and not used.

`ExecStart=/home/project/myprojectenv/bin/daphne -b 0.0.0.0 -p 8001 myproject.asgi:application`

With daphne full gunicorn configuration is like:

```
    [Unit]
    Description=gunicorn daemon
    Requires=probashigunicorn.socket
    After=network.target

    [Service]
    User=root
    Group=www-data
    WorkingDirectory=/var/www/backend/probashi_project

    # ExecStart=/var/www/backend/probashi_project/probashienv/bin/gunicorn \

    # --access-logfile - \

    # --workers 3 \

    # --bind unix:/run/gunicorn.sock \

    # probashi_backend.wsgi:application

    ExecStart=/var/www/backend/probashi_project/probashienv/bin/daphne -b 0.0.0.0 -p 8001 probashi_backend.asgi:application

    [Install]
    WantedBy=multi-user.target
```

With that, our systemd service file is complete. Save and close it now.

We can now start and enable the Gunicorn socket. This will create the socket file at `/run/myprojectgunicorn.sock` now and at boot. When a connection is made to that socket, systemd will automatically start the myprojectgunicorn.service to handle it:

```
    sudo systemctl start myprojectgunicorn.socket
    sudo systemctl enable myprojectgunicorn.socket
```

We can confirm that the operation was successful by checking for the socket file.

### Checking for the Gunicorn Socket File

Check the status of the process to find out whether it was able to start:

```
    sudo systemctl status myprojectgunicorn.socket
```

You should receive an output like this:

```
● gunicorn.socket - gunicorn socket
     Loaded: loaded (/etc/systemd/system/myprojectgunicorn.socket; enabled; vendor prese>
     Active: active (listening) since Fri 2020-06-26 17:53:10 UTC; 14s ago
   Triggers: ● myprojectgunicorn.service
     Listen: /run/myprojectgunicorn.sock (Stream)
      Tasks: 0 (limit: 1137)
     Memory: 0B
     CGroup: /system.slice/myprojectgunicorn.socket
```

Next, check for the existence of the myprojectgunicorn.sock file within the /run directory:

```
    file /run/myprojectgunicorn.sock
```

Output
`/run/myprojectgunicorn.sock: socket`

If the systemctl status command indicated that an error occurred or if you do not find the myprojectgunicorn.sock file in the directory, it’s an indication that the Gunicorn socket was not able to be created correctly. Check the Gunicorn socket’s logs by typing:

```
    sudo journalctl -u myprojectgunicorn.socket
```

Take another look at your `/etc/systemd/system/myprojectgunicorn.socket` file to fix any problems before continuing.

## Testing Socket Activation

Currently, if you’ve only started the myprojectgunicorn.socket unit, the myprojectgunicorn.service will not be active yet since the socket has not yet received any connections. You can check this by typing:

```
    sudo systemctl status myprojectgunicorn
```

Output

```
    ● myprojectgunicorn.service - gunicorn daemon
    Loaded: loaded (/etc/systemd/system/myprojectgunicorn.service; disabled; vendor preset: enabled)
    Active: inactive (dead)

```

To test the socket activation mechanism, we can send a connection to the socket through curl by typing:

```
    curl --unix-socket /run/myprojectgunicorn.sock localhost
```

You should receive the HTML output from your application in the terminal. This indicates that Gunicorn was started and was able to serve your Django application. You can verify that the Gunicorn service is running by typing:
sudo systemctl status myprojectgunicorn

Output

```
    ● myprojectgunicorn.service - gunicorn daemon
        Loaded: loaded (/etc/systemd/system/myprojectgunicorn.service; disabled; vendor preset: enabled)
        Active: active (running) since Fri 2020-06-26 18:52:21 UTC; 2s ago
    TriggeredBy: ● myprojectgunicorn.socket
    Main PID: 22914 (myprojectgunicorn)
        Tasks: 4 (limit: 1137)
        Memory: 89.1M
        CGroup: /system.slice/myprojectgunicorn.service
```

If the output from curl or the output of systemctl status indicates that a problem occurred, check the logs for additional details:

```
    sudo journalctl -u myprojectgunicorn
```

Check your `/etc/systemd/system/myprojectgunicorn.service` file for problems. If you make changes to the `/etc/systemd/system/myprojectgunicorn.service` file, reload the daemon to reread the service definition and restart the Gunicorn process by typing:

```
    sudo systemctl daemon-reload
    sudo systemctl restart myprojectgunicorn
    Make sure you troubleshoot the above issues before continuing.
```

## Configure Nginx to Proxy Pass to Gunicorn

Now that Gunicorn is set up, we need to configure Nginx to pass traffic to the process.
Start by creating and opening a new server block in Nginx’s sites-available directory:

```
    sudo nano /etc/nginx/sites-available/myproject
```

Inside, open up a new server block. We will start by specifying that this block should listen on the normal port 80 and that it should respond to our server’s domain name or IP address:

```
    server {
    listen 80;
    server_name server_domain_or_IP;
    }
```

Next, we will tell Nginx to ignore any problems with finding a favicon. We will also tell it where to find the static assets that we collected in our `~/myprojectdir/static` directory. All of these files have a standard URI prefix of `“/static”`, so we can create a location block to match those requests:

```
    server {
    listen 80;
    server_name server_domain_or_IP;

        location = /favicon.ico { access_log off; log_not_found off; }
        location /static/ {
            root /home/project/myprojectdir;
        }

    }
```

Finally, we’ll create a location `/ {}` block to match all other requests. Inside of this location, we’ll include the standard proxy_params file included with the Nginx installation and then we will pass the traffic directly to the Gunicorn socket:

```
    server {
    listen 80;
    server_name server_domain_or_IP;

        location = /favicon.ico { access_log off; log_not_found off; }
        location /static/ {
            root /home/project/myprojectdir;
        }

        location / {
            include proxy_params;
            proxy_pass http://unix:/run/myprojectgunicorn.sock;
        }

    }
```

For channel backend or socket connection we have to add upstream channels-backend :

```
upstream channels-backend {
server localhost:8001;
}
```

And proxy location look like :

```
    location / {
    include proxy_params;
    proxy_pass <http://channels-backend>;
    proxy_http_version 1.1;
    proxy_set_header Upgrade $http_upgrade;
    proxy_set_header Connection $connection_upgrade;
    proxy_redirect off;
    }
```

Now full configuration With Channel-backend looks like:

```
    map $http_upgrade $connection_upgrade {
    default upgrade;
    '' close;
    }

    upstream channels-backend {
    server localhost:8001;
    }

    server {
    listen 80;
    server_name api.probashi.info www.api.probashi.info;

        location = /favicon.ico { access_log off; log_not_found off; }
        location /static/ {
            alias /var/www/backend/probashi_project;

        }

        # Strict Transport Security
            add_header Strict-Transport-Security max-age=2592000;

            # proxy buffers
            proxy_buffers 16 64k;
            proxy_buffer_size 128k;


        location / {
                include proxy_params;
                proxy_pass http://channels-backend;
                proxy_http_version 1.1;
                proxy_set_header Upgrade $http_upgrade;
                proxy_set_header Connection $connection_upgrade;
                proxy_redirect off;
            }

    }
```

Save and close the file when you are finished. Now, we can enable the file by linking it to the sites-enabled directory:

```
    sudo ln -s /etc/nginx/sites-available/myproject /etc/nginx/sites-enabled
```

Test your Nginx configuration for syntax errors by typing:

```
    sudo nginx -t
```

If no errors are reported, go ahead and restart Nginx by typing:

```
    sudo systemctl restart nginx
```

Finally, we need to open up our firewall to normal traffic on port 80. Since we no longer need access to the development server, we can remove the rule to open port 8000 as well:

```
    sudo ufw delete allow 8000
    sudo ufw allow 'Nginx Full'
```

You should now be able to go to your server’s domain or IP address to view your application.
