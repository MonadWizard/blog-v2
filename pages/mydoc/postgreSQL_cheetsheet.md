---
title: PostgreSQL USE on Linux Terminal
keywords: PostgreSQL Bangla Tutorials, pgAdmin4, psql, database, bangla PostgreSQL, Bangla Python, Blog Bangla, Monad wizard
last_updated: July 20, 2020
# tags: [getting_started]
summary: 'Here I try to complete Basic Use of PostgreSQL Topic with short note. '
sidebar: mydoc_sidebar
permalink: postgreSQL_cheetsheet.html
folder: mydoc
---

PostgreSQL cheat-sheet 😸

## Connection

#### postgres এ Login

```
sudo -u postgres psql
```

#### alter postgres user password

```
ALTER USER postgres PASSWORD 'root';
```

#### যদি specific user as (postgres) এবং specific DataBase as (db_demo) ব্যবহার করে connect করতে চাই তাহলে

```
psql -d db_demo -U postgres -W
```

#### যদি এমন কোন DataBase এ connect করতে হয় যা আলাদা port থেকে Host করা ,তা হলে -h টাগ টি add করতে হবে

```
psql -h host -d database -U user -W

```

#### কোন কারণে যদি SSL key ব্যবহার করে DataBase এ connect করতে হয় ,তা হলে "dbname এবং sslmode" টাগ টি add করতে হবে

```
psql -U user -h host "dbname=db sslmode=require"

```

## Create user

#### create a user without any rools

```
sudo -u postgres createuser <username>
```

#### giving user a password

```
alter user <username> with encrypted password '<password>';
```

#### create user from postgres CLI with password

```
    CREATE ROLE <username> LOGIN PASSWORD '<password>' NOINHERIT CREATEDB;
```

#### Granting privileges on a database

```
grant all privileges on database <dbname> to <username> ;
```

#### view all users

```
\du
```

#### give user specific roles

-   give super User roles

```
ALTER USER demo WITH SUPERUSER;
```

-   give create database roles

```
ALTER USER demo WITH CreateDB;
```

### you may, for some reason want to do it purely via psql, then these are the three magic commands

```
CREATE DATABASE yourdbname;
CREATE USER youruser WITH ENCRYPTED PASSWORD 'yourpass';
GRANT ALL PRIVILEGES ON DATABASE yourdbname TO youruser;

```

## Drop or Delete user

1st replace or remove all dependency attribute from it by delete or reassign properties.

#### reassign owned by

```
REASSIGN OWNED BY target_user to another_user;
```

#### Drop User by

```
drop user target_user
```

## Create DataBase

#### নতুন DataBase as newbd তৈরি করতে : (generally give smaller letter)

```
create database newdb;
```

#### List available Data-Base (press q to quite)

```
\l
```

#### create database with specific user

এখানে specific user "demo" & new data-base "demobd"

```
CREATE DATABASE demodb OWNER demo;
```

#### connected to existing DataBase named newdb by

```
\c newdb;
```

or

```
\c dbname username;
```

### Drop or Delete a database that has no active connection

```
DROP DATABASE database_name;
```

## Create Schema

#### create a schema named newschema inside newdb database by

```
create schema newschema;
```

#### List available schema

```
\dn
```

## Create Table

#### create a table t1 with columns (id,password) inside schema newschema by

```
create table newschema.t1 (id integer, password CHAR(10));
```

#### List available tables

```
\dt

```

## Describe a table

#### To describe a table such as a column, type, modifiers of columns, etc., you use the following command

```
\d table_name

```

#### now see all created table by

```
select * from pg_catalog.pg_tables;
```

#### List users and their roles (To list all users and their assign roles, you use \du command

)

```
\du
```

### Command history (To display command history, you use the \s command.)

```
\s
```

If you want to save the command history to a file, you need to specify the file name followed the \s command as follows:

```
\s filename
```

### Execute psql commands from a file (In case you want to execute psql commands from a file, you use \i command as follows:)

```
\i filename
```

### Edit command in your own editor

It is very handy if you can type the command in your favorite editor. To do this in psql, you \e command. After issuing the command, psql will open the text editor defined by your EDITOR environment variable and place the most recent command that you entered in psql into the editor.

```
\e
```

After you type the command in the editor, save it, and close the editor, psql will execute the command and return the result.

### Quit psql

```
\q
```

necessary Library might need to be install for wotk with postgreSQL

```

```
