---
title: PostgreSQL and pgAdmin4 installation on Linux
keywords: PostgreSQL Bangla Tutorials, bangla PostgreSQL, Bangla Python, Blog Bangla, Monad wizard
last_updated: July 20, 2020
# tags: [getting_started]
summary: "Here I try to complete Basic Installation of PostgreSQL Topic with short note. "
sidebar: mydoc_sidebar
permalink: postgreSQL_basic_linux.html
folder: mydoc
---

PostgreSQL is a powerful, open source object-relational database. Installing PostgreSQL on Ubuntu was always a problem for me when I started using PostgreSQL. The problem was in setting up the root user credentials. I have tried lot of commands with no success. After so many tries I found the correct command to use. I'm documenting the steps here which will help some newbies trying to install PostgreSQL on Ubuntu.

### Versions Used

* Ubuntu - 20.04
* PostgreSQL - 12
* pgAdmin4 - 4.24


### Step 1: Install PostgreSQL

You can install PostgreSQL 12 using the command

    sudo apt install postgresql


### Step 2: Set root user credentials

Login to PostgreSQL shell using the command

    sudo -u postgres psql

Then set root user credentials using the command

    ALTER USER postgres PASSWORD 'newpassword';

You can now exit the PostgreSQL shell using the command quit.


Henceforth you can login to the PostgreSQL shell using the command

    psql -U postgres -h localhost

and the password you set in the previous step.


you can see all database using the command

    \l



### Step 3: Create multiple users (optional)

You can the list the users in PostgreSQL using the command

    \du


You can create user using the command

    CREATE USER arul WITH CREATEDB LOGIN ENCRYPTED PASSWORD 'admin';

You should also create a database with the same name as the user. Create database using the command

    CREATE DATABASE arul;

You can grant access to existing databases to the user using the command

    GRANT ALL PRIVILEGES ON DATABASE codingpub TO arul;

Using the above command, we have granted access to the database codingpub to the user arul.



### Step 4: Install pgAdmin (recommended)

pgAdmin is the most popular and feature rich Open Source administration tool for PostgreSQL. Installing pgAdmin is optional but recommended. You can try an online demo of pgAdmin4 here.

Create the repository configuration file:

    curl https://www.pgadmin.org/static/packages_pgadmin_org.pub | sudo apt-key add

    sudo sh -c 'echo "deb https://ftp.postgresql.org/pub/pgadmin/pgadmin4/apt/$(lsb_release -cs) pgadmin4 main" > /etc/apt/sources.list.d/pgadmin4.list && apt update'

pgAdmin4 can be installed in two modes:

To install desktop mode, use the command:

    sudo apt install pgadmin4-desktop

To install web mode, use the command:

    sudo apt install pgadmin4-web

To install both, use the command:

    sudo apt install pgadmin4

To configure web mode, run the command:

    sudo /usr/pgadmin4/bin/setup-web.sh

and follow the on-screen instructions. This is required only one time after the installation.

Note that in both the modes, pgAdmin4 opens in a web browser. How you open pgAdmin4 varies based on the mode you select.

Now we have installed PostgreSQL and pgAdmin successfully. Feel free to post your comments.







