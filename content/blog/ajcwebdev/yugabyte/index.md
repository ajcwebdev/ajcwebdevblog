---
title: yugabyte
date: "2020-06-21"
description: open source, high-performance, distributed SQL database for global, internet-scale apps
---

![yugabyte-logo](https://cdn.substack.com/image/fetch/w_1456,c_limit,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fbucketeer-e05bbc84-baa3-437e-9518-adb32be77984.s3.amazonaws.com%2Fpublic%2Fimages%2Ff6ec9dfd-916e-49b6-8add-a65c2fa6ae7e_1200x627.jpeg)

YugabyteDB is the open source, high-performance, distributed SQL database for global, internet-scale apps. It's design goals include:

## Consistency
YugabyteDB offers strong consistency guarantees in the face of a variety of failures. It supports distributed transactions.

![Image](https://sedaily-topics.s3.amazonaws.com/topic_images/0_0751087199757039.png)

### CAP theorem

##### YugabyteDB is a CP database (consistent and partition tolerant), but achieves very high availability.

![Image](https://sedaily-topics.s3.amazonaws.com/topic_images/0_46449082061705016.png)

##### The architectural is similar to Spanner, also a CP system.

![Image](https://sedaily-topics.s3.amazonaws.com/topic_images/0_31791606398132966.jpg)

##### The description about Spanner is just as valid for YugabyteDB.

![Image](https://sedaily-topics.s3.amazonaws.com/topic_images/0_16166467451607391.jpg)

No system provides 100% availability, so the pragmatic question is whether or not the system delivers availability that is so high that most users no longer have to be concerned about outages. Given there are many sources of outages if YugabyteDB is an insignificant contributor to downtime users are correct to not worry about it.

### Multi-row ACID transactions
Supports multi-row transactions with both Serializable and Snapshot isolation.

## Query APIs
* Does not reinvent data client APIs
* Wire-compatible with existing APIs
* Extends functionality

### YSQL
[YSQL](https://docs.yugabyte.com/latest/api/ysql/) is a fully-relational SQL API that is wire compatible with the SQL language in PostgreSQL. It is best fit for RDBMS workloads that need horizontal write scalability and global data distribution while also using relational modeling features such as:
* JOINs
* Distributed transactions
* Referential integrity such as foreign keys

![Image](https://sedaily-topics.s3.amazonaws.com/topic_images/0_6846242403809615.png)

### YCQL
[YCQL](https://docs.yugabyte.com/latest/api/ycql/) has its roots in the [Cassandra Query Language](https://cassandra.apache.org/doc/latest/cql/) and is a SQL-based flexible-schema API fit for internet-scale OLTP apps needing:
* A semi-relational API highly
* Optimization for write-intensive applications
* Blazing-fast queries

## Performance
Written in C++ to ensure high performance and the ability to leverage large memory heaps (RAM) as an internal database cache. It is optimized primarily to run on SSDs and NVMe drives. Designed for high write throughput, high client concurrency, high data density, and ever growing event data.

## Geo-distributed deployments

![Image](https://sedaily-topics.s3.amazonaws.com/topic_images/0_12975404508546284.png)

### Multi-region configurations
YugabyteDB should work well in deployments where the nodes of the cluster span:

* Single zone
* Multiple zones
* Multiple regions that are geographically replicated
* Multiple clouds (both public and private clouds)

To achieve this client drivers across the various languages should be:

* Cluster-aware - handle node failures seamlessly
* Topology-aware - route traffic seamlessly

![Image](https://sedaily-topics.s3.amazonaws.com/topic_images/0_9991572357087302.png)

## Cloud native architecture

### Run on commodity hardware
* Run on any public cloud or on-premises data center including commodity hardware on bare metal machines, VMs or containers.
* No external dependencies such as atomic clocks but can utilize one if available.

### Kubernetes ready
Should work natively in Kubernetes and other containerized environments as a stateful application.

### Open source
YugabyteDB is open source under the very permissive Apache 2.0 license.