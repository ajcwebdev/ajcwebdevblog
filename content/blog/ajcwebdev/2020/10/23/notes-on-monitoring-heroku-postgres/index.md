---
title: notes on monitoring heroku postgres
date: "2020-10-23"
description: notes on monitoring heroku postgres
---

# Database Metrics

## `db_size`
* Number of bytes contained in the database
* Includes all table and index data on disk, including database bloat

If your Postgres database grows past the size allotted for your plan, you will receive a warning email with directions on how fix the issue. In some cases an enforcement date will be set for when you will be allowed only a single database connection and access will be restricted to READ, DELETE, and TRUNCATE access until the database is back under the plan limit.

Heroku recommends setting a warning alert when your database gets to 80% of the allotted size for your plan and a critical alert when it gets to 90% of the allotted size.

As you approach maximum size you can either upgrade your plan or delete data to stay within plan limits.

## `tables`
* Number of tables in the database

## `active-connections`
* Number of connections established on the database

Heroku Postgres enforces a connection limit in order to optimize Postgres memory usage and scaling.

For Heroku Postgres plans tier-3 and higher there is a hard limit of 500 connections. Once that limit is reached no new connections can be created.

There are two strategies for setting up alerts based on database connection counts:

* **Set up an alert for sudden, large changes to the current connection count.** Big changes from baseline connection numbers could be a sign of increased query and/or transaction run times. Alerting thresholds will be dependent on your application’s connection count range, assessed under normal operating conditions. Consider +50/+100 over your normal daily maximum.
* **Set up an alert for when the connection count approaches its hard maximum.** For tier-3 plans and higher, the maximum is 500 connections, so 400 and 450 are good warning and critical numbers to start with here.

If you are routinely approaching your connection limit, consider using connection pooling.

## `current_transaction`
* Current transaction ID
* Can be used to track writes over time

## `index-cache-hit-rate`
* Ratio of index lookups served from shared buffer cache, rounded to five decimal points
* Heroku recommends a value of 0.99 or greater if possible
* If your index hit rate is consistently less than 0.99, you should investigate your Expensive Queries or you may need to upgrade your database plan for more RAM

## `table-cache-hit-rate`
* Ratio of table lookups served from shared buffer cache, rounded to five decimal points
* Heroku recommends a value of 0.99 or greater if possible
* If your table hit rate is consistently less than 0.99, you may need to upgrade your database plan for more RAM

## `waiting-connections`
* Number of connections waiting on a lock to be acquired
* If many connections are waiting, this can be a sign of mishandled database concurrency

Set up an alert for when there are any connections waiting for five consecutive minutes. You can use the pg-extras CLI plugin to help identify queries that are preventing other operations from taking place.

The blocking queries can then be terminated in order to resolve lock contention. Additionally, knowing what statements cause blocks can help to identify application code that can be optimized to reduce locks.

## `memory-postgres`
* Approximate amount of memory used by your database’s Postgres processes in kB
* Includes shared buffer cache as well as memory for each connection

## `follower-lag-commits`
* Replication lag, measured as the number of commits that this follower is behind its leader
* Replication is asynchronous so a number greater than zero may not indicate an issue, however an increasing value deserves investigation
* This metric is only published for follower databases

# Server Metrics

## `load-avg-1m`, `load-avg-5m`, `load-avg-15m`
* The average system load over a period of 1 minute, 5 minutes and 15 minutes, divided by the number of available CPUs
* A `load-avg` of 1.0 indicates that, on average, processes were requesting CPU resources for 100% of the timespan; this number includes I/O wait
* For databases that have burstable performance, a baseline load average is guaranteed

The `load-avg` metric shows average CPU load over the indicated periods. Heroku’s reported load metrics are normalized by dividing the system load by the number of CPUs.

A load average of 1.0 over a given time window indicates full utilization of all CPUs, a load over 1.0 indicates that processes had to wait for CPU time in the given window (with higher values indicating more time spent by processes waiting), and values under 1.0 indicate that CPUs spent time idle during the given window. If this value is high, you will get less consistent query execution times and longer wait times.

Since values over 1.0 indicate over-utilization, you will want to know before the load gets to that number. Set up alerts for when this `load-avg` reaches 0.8 (warning) and 0.9 (critical).

Check current activity with the `pg:ps` command for cpu-intensive queries. Additionally check IOPS, as exceeding provisioned IOPS will cause processes to need to wait on I/O to become available before they can process. If you are consistently seeing high values for `load-avg`, then it may be time to upgrade to a larger Heroku Postgres plan. Before doing that, or if you’re already on the largest plan, look to tuning expensive queries to reduce the amount of processing work done on the database server and/or data read from disk.

## `read-iops`, `write-iops`
* Number of read or write operations in I/O sizes of 16KB blocks

## `memory-total`
* Total amount of server memory available

## `memory-free`
* Amount of free memory available in kB

## `memory-cached`
* Amount of memory being used the OS for page cache, in kB

## `wal-percentage-used`
* The percentage of wal used, healthy below 80%