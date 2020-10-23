---
title: notes on monitoring heroku postgres
date: "2020-10-23"
description: notes on monitoring heroku postgres
---

db_size
* The number of bytes contained in the database. This includes all table and index data on disk, including database bloat.

tables
* The number of tables in the database.

active-connections
* The number of connections established on the database.

current_transaction
* The current transaction ID, which can be used to track writes over time.

index-cache-hit-rate
* Ratio of index lookups served from shared buffer cache, rounded to five decimal points. Heroku recommends a value of 0.99 or greater if possible. If your index hit rate is consistently less than 0.99, you should investigate your Expensive Queries or you may need to upgrade your database plan for more RAM.

table-cache-hit-rate
* Ratio of table lookups served from shared buffer cache, rounded to five decimal points. Heroku recommends a value of 0.99 or greater if possible. If your table hit rate is consistently less than 0.99, you may need to upgrade your database plan for more RAM.

waiting-connections
* Number of connections waiting on a lock to be acquired. If many connections are waiting, this can be a sign of mishandled database concurrency.

memory-postgres
* Approximate amount of memory used by your database’s Postgres processes in kB. This includes shared buffer cache as well as memory for each connection.

follower-lag-commits
* Replication lag, measured as the number of commits that this follower is behind its leader. Replication is asynchronous so a number greater than zero may not indicate an issue, however an increasing value deserves investigation. Read more in Monitoring Followers. This metric is only published for follower databases.