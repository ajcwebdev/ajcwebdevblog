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

# Finding Slow Queries

## Logging

### `log_min_duration_statement`

Causes the duration of each completed statement to be logged if the statement ran for at least the specified number of milliseconds. For example, if you set it to 250ms then all SQL statements that run 250ms or longer will be logged.

Enabling this parameter can be helpful in tracking down unoptimized queries in your applications. Only superusers can change this setting.

### `log_line_prefix`

`printf`-style string that is output at the beginning of each log line.

* Timestamp
* Process ID
* Session Line Number
* Logged in User
* Database logged in to
* Application name
* Remote host

### `log_checkpoints`

Causes checkpoints and restartpoints to be logged in the server log. Some statistics are included in the log messages, including the number of buffers written and the time spent writing them.

### `log_connections`

Causes each attempted connection to the server to be logged, as well as successful completion of client authentication.

### `log_disconnections`

Causes session terminations to be logged. The log output provides information similar to `log_connections`, plus the duration of the session.

### `log_lock_waits`

Controls whether a log message is produced when a session waits longer than `deadlock_timeout` to acquire a lock. This is useful in determining if lock waits are causing poor performance.

### `log_temp_files`

Controls logging of temporary file names and sizes. Temporary files can be created for sorts, hashes, and temporary query results. If enabled by this setting, a log entry is emitted for each temporary file when it is deleted. A value of zero logs all temporary file information, while positive values log only files whose size is greater than or equal to the specified amount of data. If this value is specified without units, it is taken as kilobytes.

### `log_autovacuum_min_duration`

Causes each action executed by autovacuum to be logged if it ran for at least the specified number of milliseconds. Setting this to zero logs all autovacuum actions. Minus-one (the default) disables logging autovacuum actions. For example, if you set this to 250ms then all automatic vacuums and analyzes that run 250ms or longer will be logged. In addition, when this parameter is set to any value other than -1, a message will be logged if an autovacuum action is skipped due to the existence of a conflicting lock. Enabling this parameter can be helpful in tracking autovacuum activity.

## Log Analysis

### pgBadger

## Viewing Active Queries

### `pg_stat_statements`

The `pg_stat_statements` module provides a means for tracking planning and execution statistics of all SQL statements executed by a server.

The module must be loaded by adding `pg_stat_statements` to `shared_preload_libraries` in `postgresql.conf`, because it requires additional shared memory. This means that a server restart is needed to add or remove the module.

The statistics gathered by the module are made available via a view named `pg_stat_statements`. This view contains one row for each distinct database ID, user ID and query ID (up to the maximum number of distinct statements that the module can track).

# USE Method

For every resource, check utilization, saturation, and errors.
It's intended to be used early in a performance investigation, to identify systemic bottlenecks.

resource: all physical server functional components (CPUs, disks, busses, ...) [1]
utilization: the average time that the resource was busy servicing work [2]
saturation: the degree to which the resource has extra work which it can't service, often queued
errors: the count of error events

# pgbouncer

pgbouncer is a PostgreSQL connection pooler that aims to lower the performance impact of opening new connections to PostgreSQL. Any target application can be connected to pgbouncer as if it were a PostgreSQL server, and pgbouncer will create a connection to the actual server, or it will reuse one of its existing connections.

In order not to compromise transaction semantics for connection pooling, pgbouncer supports several types of pooling when rotating connections:

### Session pooling

* Most polite method and default method
* When a client connects, a server connection will be assigned to it for the whole duration the client stays connected
* When the client disconnects, the server connection will be put back into the pool

### Transaction pooling

* A server connection is assigned to a client only during a transaction
* When PgBouncer notices that transaction is over, the server connection will be put back into the pool

### Statement pooling

* Most aggressive method
* The server connection will be put back into the pool immediately after a query completes
* Multi-statement transactions are disallowed in this mode as they would break

# What Needs to be Monitored?

### Queries/SQL

* Throughput
* Latency
* Concurrency/load
* Errors

### Postgres Server

* DML
* DDL
* Logs
* Wait-time
* Users
* Objects
* Backups
* Replication

### OS and Hardware

* I/O
* Memory
* Network
* CPU