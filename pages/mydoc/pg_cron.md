---
title: Pg_cron for schedule handle on Database layer.
keywords: pg_cron Bangla Tutorials, pg_cron postgresql, pgcron psql, database, bangla PostgreSQL, Bangla Python, Blog Bangla, Monad wizard
last_updated: July 21, 2022
# tags: [getting_started]
summary: 'Here I try to complete Basic Use of pg_cron Topic with short note. '
sidebar: mydoc_sidebar
permalink: pg_cron.html
folder: mydoc
---

# pgcron doc

Pg_cron একটি cron-based job scheduler যা PostgreSQL(9.5 or higher) এর ভেতর একটি Database extension হিসেবে run করে। Pg_cron ব্যবহার করে specific সময় পর পর নির্দিষ্ট sql query কে postgresql এ execute করা যায়।

for an example application এর people suggation portion থেকে user1 যদি user13 কে unmatch করে, তবে user1 তার suggestion portion এবং search people portion এ user13 কে দেখতে পাবে না এবং user13 ও তার suggestion portion এবং search people portion এ user1 কে দেখতে পাবে না।

According to business case, unmatched করা users গুলো 40 days এর বেশি unmatched থাকবে না। তারা আবার suggestion টেবিল এবং search people portion এ seen হবে।  
যে সব user এর unmatched date ৪০ দিন হয়েছে তাদেরকে unmatch table থেকে remove করে দেয়ার opperation টি postgreSQL এর under এ সম্পূর্ণ হয়। প্রতিদিন রাত ৩ টার সময় user_unmatches table এ PostgreSQL একটি query অপারেশান execute করবে এবং current date-time এর থেকে 40 days পূর্বে create হওয়া row/user information গুলো remove করে দিবে।

উপরোক্ত operation টি একটি scheduler operation যা postgreSQL এর under এ pg_cron এর দ্বারা execute হয়। PostgreSQL এ Pg_cron configure করার জন্য নিচের instruction follow করতে হবে ।

Installing Pg_cron:
Red Hat, CentOS, Fedora, and Amazon Linux এর সংঘে PostgreSQL 12 এ pg_cron extension install :

    sudo yum install -y pg_cron_12

install on Debian, and Ubuntu with PostgreSQL 12 using apt.postgresql.org:

    sudo apt-get -y install postgresql-12-cron

Setting up pg_cron:
Pg_cron এর জন্য postgreSQL এর background worker enable করার জন্য shared_preload_libraries তে pg_cron কে উল্লেখ করতে হবে । server যদি hot standby mode এ থাকে তবে pg_Cron run হবে না। কিন্তু যখন server start হবে pg_cron automatically start হবে।

# add to postgresql.conf

# required to load pg_cron background worker on start-up

    shared_preload_libraries = 'pg_cron'

By default, pg_cron এর background worker তার metadata tables গুলো "Postgres" database এ তৈরি করে।
তাই যে database এর table এ scheduler operation টি execute হবে সেই database name টি postgresql.conf file এর cron.database_name configuration parameter এ উল্লেখ করতে হবে।

# add to postgresql.conf

# optionally, specify the database in which the pg_cron background worker should run (defaults to postgres)

    cron.database_name = 'database_name’

Configuration part শেষ হয়েছে। এখন postgreSQL restart করার পর ‘CREATE EXTENSION pg_cron’ ব্যবহার করে pg_cron function এবং metadata table তৈরি করতে পারা যায়।

-- run as superuser:
CREATE EXTENSION pg_cron;

-- optionally, grant usage to regular users:
GRANT USAGE ON SCHEMA cron TO postgre_user_name;

Important: by default pg_Cron, libpq ব্যবহার করে একটি নতুন connection কে local database এ তৈরি করে। যা pg_hba.conf থেকে allowed থাকতে হয়। database এর user authentication এ trust enable থাকতে হবে যেন localhost এ cron job running থাকে । এই জন্য postgreuser এর password টি .pgpass file এ রাখতে হবে, যা libpq ব্যবহার করে connection open করবে।

.pgpass এই file এ postgresql এর credential নিম্ন রূপে থাকে,

# hostname:port:database:username:password

    localhost:5432:demo_db:postgres:postgres

pg_cron এর background workers এর number of concurrent job এর limit কে max_worker_processes ব্যবহার করে setting করতে হবে।

# Schedule jobs via background workers instead of localhost connections

    cron.use_background_workers = on

# Increase the number of available background workers from the default of 8

    max_worker_processes = 20

এছাড়া Unix domain socket directory থেকে hostname কে trust permission দিয়ে pg_cron এর libpq এর connection established করা যায়।

Pg_cron কে operational করার জন্য নিচের step গুলো follow করতে হবে।

Step 1: demo_db এই database এ pg_cron extension নিয়ে কাজ করার জন্য at first postgreSQL এ CLI terminal থেকে connect হতে হবে।

    psql -h localhost -U postgres demo_db;

Step 2: step 1 এ connect থাকা অবস্থাতে demo_db database এ Pg_cron এর plug-in create করতে হবে।

    CREATE EXTENSION pg_cron;
    GRANT USAGE ON SCHEMA cron TO postgre_user_name;

Step 1 এ connect থাকা অবস্থাতে demo_db থেকে create করা extension remove করার জন্য নিচের command run করতে হবে।  
DROP EXTENSION pg_cron;

Step 1 এ connect থাকা অবস্থাতে pg_cron থেকে schedule করা সকল queryগুলো নিচের query দ্বারা দেখা যায়।

```
    select * from cron.job;

    jobid |  schedule   |   command                       | nodename  | nodeport |  database   | username | active | jobname
    -------+----------------+----------------------------------+---------------+-------------+----------------+--------------+--------+---------

```

Step 3: Step 1 এ connect থাকা অবস্থাতে pg_cron এ postgreSQL এর query টি shedule করার জন্য নিচের query execute করতে হবে।
SELECT cron.schedule('0 3 \* \* \*', $$DELETE FROM public.auth_user_app_user_unmatch WHERE user_unmatch_created_at < now() - interval '40 days'$$);

Schedule query টির structure SELECT cron.schedule('\* \* \* \* \*', $$<PostgreSQL query>$$);

```
    ┌───────────── min (0 - 59)
    │ ┌────────────── hour (0 - 23)
    │ │ ┌─────────────── day of month (1 - 31)
    │ │ │ ┌──────────────── month (1 - 12)
    │ │ │ │ ┌───────────────── day of week (0 - 6) (0 to 6 are Sunday to
    │ │ │ │ │ Saturday, or use names; 7 is also Sunday)
    │ │ │ │ │
    │ │ │ │ │

    * * * * *
```

Pg_cron এর কোন schedule কে unschedule করতে হলে নিচের command টি Step 1 এ connect থাকা অবস্থাতে run করতে হবে।  
 SELECT cron.unschedule(jobid);
Or
SELECT cron.unschedule(jobid) FROM cron.job;

    SELECT \* FROM cron.job; থেকে Jobid নিয়ে সেই jobid user করে unschedule করতে হবে।

```

    jobid | schedule | command | nodename | nodeport | database | username | active | jobname
    -------+-------------+-----------------------+-----------+----------+-------------+----------+--------+---------
    3 | 0 3 \* \* \* | DELETE FROM public.auth_user_app_user_unmatch WHERE user_unmatch_created_at < now() - interval '2 MINUTE' | localhost | 5432 | demo_db | postgres | t |
    (1 rows)

```

উদাহর সরূপ
SELECT cron.unschedule(3); ব্যবহার করে schedule টি unschedule করা যায়।
