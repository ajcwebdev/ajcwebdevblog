---
title: dynamo
date: "2020-06-26"
description: fast and flexible nosql database service for any scale
---

These are the notes I'm taking as I'm going through [Alex DeBrie's DynamoDB guide](https://www.dynamodbguide.com/) and all credit should go to him. If you find this valuable you can buy [The DynamoDB Book](https://www.dynamodbbook.com).

## DynamoDB is a hosted NoSQL database by Amazon Web Services

* Reliable performance as it scales
* Managed experience, no SSH-ing into servers to upgrade crypto libraries
* Small, simple API for simple key-value access as well as more advanced query patterns

### Good fit for:

#### Apps with large data and strict latency requirements
* As your amount of data scales, JOINs and advanced SQL operations can slow down your queries
* Dynamo's queries have predictable latency up to any size, including over 100 TBs

#### Serverless applications on AWS Lambda
* AWS Lambda provides auto-scaling, stateless, ephemeral compute in response to event triggers.
* DynamoDB is accessible via an HTTP API and performs authentication & authorization via IAM roles, good for building Serverless applications.

#### Data sets with simple, known access patterns
* For generating recommendations and serving them to users DynamoDB's key-value access patterns are fast and reliable.

# Tables, Items, and Attributes

## Table

### A *table* is a grouping of data records.

* You might have a Users table to store data about your users, and an Orders table to store data about your users' orders.
* This concept is similar to a table in a relational database or a collection in MongoDB.

## Item

### An *item* is a single data record in a table.

* Each item in a table is uniquely identified by the stated primary key of the table.
* In your Users table, an item would be a particular User.
* An item is similar to a row in a relational database or a document in MongoDB.

## Attributes

### *Attributes* are pieces of data attached to a single item.

Could be a simple Age attribute that stores the age of a user.
* Comparable to a column in a relational database or a field in MongoDB.
* Does not require attributes on items except for attributes that make up your primary key.

## Primary Key

Each item in a table is uniquely identified by a primary key.
* The primary key definition must be defined at the creation of the table.
* The primary key must be provided when inserting a new item.

Two types of primary key:
* *Simple primary key* - just a partition key
* *Composite primary key* - a partition key and a sort key

### Simple primary key

Similar to key-value stores (Memcached) or accessing rows in a SQL table by a primary key.
* Example: a Users table with a Username primary key.

### Composite primary key

More complex, you specify both a partition key and a sort key to (wait for it) sort items with the same partition.
* Example: an Orders table for recording customer orders on an e-commerce site. The partition key would be the CustomerId, and the sort key would be the OrderId.

*Each item in a table is uniquely identified by a primary key*, even with the composite key. When using a table with a composite primary key, you may have multiple items with the same partition key but different sort keys. You can only have one item with a particular combination of partition key and sort key.

The composite primary key enables sophisticated query patterns, including:
* Grabbing all items with the given partition key
* Using the sort key to narrow the relevant items for a particular query.

## Secondary Indexes

Primary key uniquely identifies an item in a table. You can make queries against the table using the primary key. Sometimes you have additional access patterns that would be inefficient with your primary key. *Secondary indexes* enable these additional access patterns.

### Local secondary index

A local secondary index uses the same partition key as the underlying table but a different sort key.
* To take our Order table example from the previous section, imagine you wanted to quickly access a customer's orders in descending order of the amount they spent on the order.
* You could add a local secondary index with a partition key of CustomerId and a sort key of Amount, allowing for efficient queries on a customer's orders by amount.

### Global secondary index

A global secondary index can define an entirely different primary key for a table. This could mean:
* Setting an index with just a partition key for a table with a composite primary key.
* Using completely different attributes to populate a partition key and sort key.

With the Order example above, we could have a global secondary index with a partition key of OrderId so we could retrieve a particular order without knowing the CustomerId that placed the order.

## Read and Write Capacity

With MySQL, Postgres, or MongoDB you provision a particular server to run your database. You'll need to choose your instance size:
* how many CPUs do you need
* how much RAM
* how many GBs of storage

With DynamoDB you provision read and write capacity units. These units allow a given number of operations per second. This is a different pricing paradigm than the instance-based world. Pricing more closely reflects actual usage.

DynamoDB has autoscaling of read and write capacity units making it easier to scale during peak times while saving money by scaling down when your users are asleep.