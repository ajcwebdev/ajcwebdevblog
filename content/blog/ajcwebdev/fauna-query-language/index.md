---
title: fauna query language
date: "2020-08-11"
description: native api for querying fauna
---

The Fauna Query Language (FQL) is the native API for querying FaunaDB. While not a general-purpose programming language, it provides much of the functionality expected from one. It allows for complex, precise manipulation and retrieval of data stored within FaunaDB.

A query is executed by submitting it to a FaunaDB cluster, which computes and returns the result. Query execution is transactional: No changes are committed if something goes wrong. If a query fails, an error response is returned instead of a result.

FQL operates primarily on the schema types provided by FaunaDB, which include:
* Documents
* Collections
* Indexes
* Sets
* Databases

For a quick reference to all FQL functions see the [FQL cheat sheet](https://docs.fauna.com/fauna/current/api/fql/cheat_sheet).

# Data types

FQL uses an enhanced Javascript Object Notation (JSON) format for storing and communicating data. All of JSON’s basic types are supported, including Number, String, Boolean, Array, and Object.

In addition to the basic types, FQL supports the following types beyond those native to JSON:
* ***Byte***: Denotes a Base64-encoded string representing a byte array.
* ***Date***: Denotes a date, with no associated time zone.
* ***Page***: Contains an array of results and other decorated elements.
* ***Query***: Denotes a query expression object.
* ***Ref***: Denotes a resource reference. Refs may be extracted from documents, or constructed using the `Collection`, `Database`, `Function`, `Index`, or `Role` functions, or the general-purpose `Ref` function.
* ***Set***: Denotes a set identifier. A set is a group of tuples, typically representing resources or index `terms`, that are in a specific order.
* ***Timestamp***: Stores an instant in time expressed as a calendar date and time of day in UTC (usually written as `ts`).

# Databases

Databases are defined as documents of type ***database***. Databases exist within the system-global root database context. Aside from keys, all other documents exist within the context of a specific database. All queries are limited to a single database as well, and cannot span across databases.

|Field|Type|Definition and Requirements|
|-----|----|---------------------------|
|`name`|String|Cannot be `events`, `sets`, `self`, `documents`, or `_`.|
|`api_version`|String| The default API version for requests made to this database. Defaults to 2.7.|
|`priority`|Number|A priority between 1 and 500, inclusive. Defaults to 1.|
|`data`|Object|A JSON object. Optional.|

# Collections

A database’s schema is defined by its collections, which are similar to tables in other databases. To create a collection, create a document of type ***collection***. Once the collection is defined, it is possible to create documents within the collection using the query API.

|Field|Type|Definition and Requirements|
|-----|----|---------------------------|
|`name`|String|Cannot be `events`, `sets`, `self`, `documents`, or `_`.|
|`data`|Object|A JSON object. Optional.|
|`history_days`|Number|Document history is retained for at least this many days. Defaults to 30 days.|
|`ttl_days`|Number|Documents are deleted this many days after their last write. Optional.|
|`permissions`|Object|Optional.|

### Create Collection

The `CreateCollection` function is used to create a collection that groups documents. Once the collection has been created, it is possible to create documents within the collection.

The following query creates a collection called "boons" with defaults:

```javascript
client.query(q.CreateCollection({ name: 'boons' }))
.then((ret) => console.log(ret))
```

```
{ ref: Ref(id=boons, collection=Ref(id=collections)),
  ts: 1527274777496292,
  history_days: 30,
  name: 'boons' }
```

# Documents

Every record, of any kind, in a FaunaDB database is stored as an object called a ***document***. Documents are made up of fields and their associated value, just like a JSON object. The value for any key can itself be a document.
* Every document belongs to a specific collection, similar to a table in other database systems, which groups similar documents together. Documents within collections are not required to share the same structure.
* Collections belong to a specific database, which is the contents of all other schemas in FaunaDB.

Even the definitions of Databases, Collections, Keys, Indexes, and user-defined functions, are all documents. They exist within internal FaunaDB collections of the same name.

All documents have a set of common characteristics:
* Documents have an identifier called a ***ref*** that encodes its collection along with a unique id. The combination of these attributes forms a unique identifier for the document within the scope of the database in which it is stored.
* User-specified documents have a timestamp that identifies when the document was most recently updated. FaunaDB documents are versioned and the versions are distinguished using the timestamp.
* Documents can have an optional ttl field (time-to-live), which is a timestamp indicating when the document should be removed.
* Documents are manipulated with the same query language functions. Documents returned by queries are represented as JSON objects. Within a query, a document’s fields may be accessed using the `Select` function.

To separate the ref and timestamp from user-defined fields, FaunaDB wraps each user-specified document in a metadata document for storage, and user-specified data appears in the `data` field.

For example, when a blog post document is created, it is stored as:

```javascript
{
  ref: Ref(Collection("posts"), "227576404750893579"),
  ts: 1553292644000000,
  data: {
    title: 'My blog post',
    tags: [ 'post', 'popular', 'blog' ],
    body: "Lorem ipsum..."
  }
}
```

### Create

The `Create` function adds a new document to a collection.

The following query creates a document by providing a reference to the collection "spells" and a `param_object` with a `data` field. The `data` field contains the user data to be inserted for this document.

```javascript
client.query(
  q.Create(
    q.Collection('spells'),
    {
      data: {
        name: 'Mountainous Thunder',
        element: 'air',
        cost: 15,
      },
    },
  )
)
.then((ret) => console.log(ret))
```

```
{ ref:
  Ref(id=181388642581742080, collection=Ref(id=spells, collection=Ref(id=collections))),
  ts: 1527274715273882,
  data: { name: 'Mountainous Thunder', element: 'air', cost: 15 } }
```

### Read

The `Get` function retrieves a single document identified by `ref`.

The following query retrieves an document by providing a reference to the collection named "spells" at a specific id:

```javascript
client.query(
  q.Get(q.Ref(q.Collection('spells'), '181388642046968320'))
)
.then((ret) => console.log(ret))
```

```
{ ref: Ref(id=181388642046968320, collection=Ref(id=spells, collection=Ref(id=collections))),
  ts: 1526677786695156,
  data:
   { name: "Fire Beak",
     element: [ "air", "fire" ],
     spellbook: Ref(id=181388642139243008, collection=Ref(id=spellbooks, collection=Ref(id=collections))) } }
```

### Update

The `Update` operation only modifies the specified fields in the documents pointed to by `ref`. Updates are partial, and only modify values that are specified in the param_object.

The following query updates the document by changing the `name` field to the value "Mountains’s Thunder" and removing the `cost` field from the document.

```javascript
client.query(
  q.Update(
    q.Ref(q.Collection('spells'), '181388642581742080'),
    {
      data: {
        name: 'Mountain\'s Thunder',
        cost: null,
      },
    },
  )
)
.then((ret) => console.log(ret))
```

```
{ ref:
   Ref(id=181388642581742080, collection=Ref(id=spells, collection=Ref(id=collections))),
  ts: 1527276015058883,
  data: { name: 'Mountain\'s Thunder', element: [ 'air' ] } }
```

### Delete

The `Delete` function removes a document. This includes user-created documents, plus system documents for Collections, Indexes, Databases, etc.

The query below removes the document pointed at by the reference.

```javascript
client.query(q.Delete(q.Ref(q.Collection('spells'), '181388642581742080')))
.then((ret) => console.log(ret))
```

```
{ ref:
   Ref(id=181388642581742080, collection=Ref(id=spells, collection=Ref(id=collections))),
  ts: 1527275280180078,
  data:
   { name: 'Mountain\'s Thunder',
     element: [ 'air', 'earth' ],
     cost: 10 } }
```

# Indexes

Indexes allow for the organization and retrieval of documents by attributes other than their References. They are defined as documents within the system ***indexes*** collection. An index is a database entity that facilitates efficient data lookups.
* A Set is a sorted group of immutable data from a collection.
* An Index is a group of sets within a collection.

|Field|Type|Definition and Requirements|
|-----|----|---------------------------|
|`name`|String|The logical name of the index. Cannot be `events`, `sets`, `self`, `documents`, or `_`.|
|`source`|Reference or Array|A Collection reference, or an array of one or more source objects describing source collections and (optional) binding fields.|
|`terms`|Array|Optional - An array of Term objects describing the fields that should be searchable. Indexed terms can be used to search for field values, via the Match function.|
|`values`|Array|Optional - An array of Value objects describing the fields that should be reported in search results.|
|`unique`|Boolean|Optional - If `true`, maintains a unique constraint on combined terms and values.|
|`serialized`|Boolean|Optional - If `true`, writes to this index are serialized with concurrent reads and writes.|
|`permissions`|Object|Optional - Indicates who is allowed to read the index.|
|`data`|Object|Optional - This is user-defined metadata for the index. It is provided for the developer to store information at the index level.|

### Example Index

The simplest index is called a "collection" index; it has no `terms` or `values` defined. This means that the index includes all documents with no search terms, and that the index returns the references to each indexed document.

Such an index can be created with just a `name` and a `source` collection:

```javascript
client.query(
  q.CreateIndex({
    name: 'new-index',
    source: q.Collection('spells'),
  })
)
.then((ret) => console.log(ret))
```

```
{ ref: Ref(id=new-index, collection=Ref(id=indexes)),
  ts: 1527275052756370,
  active: false,
  partitions: 8,
  name: 'new-index',
  source: Ref(id=spells, collection=Ref(id=collections)) }
```

### Source Objects

Source objects describe the source collection of index entries and, optionally, bindings.

The following example demonstrates the structure of a source object, which includes an example binding object:

```javascript
client.query({
  source: {
    collection: q.Collection('collection'),
    fields: {
      binding1: q.Query(
        q.Lambda(
          'document',
          q.Select(['data', 'field'], q.Var('document'))
        )
      ),
    },
  },
})
.then((ret) => console.log(ret))
```

```
{ source:
   { collection: Collection("collection"),
     fields:
      { binding1:
         Query(Lambda("document", Select(["data", "field"], Var("document")))) } } }
```

### Binding Objects

A binding object contains field names bound to pure, single-argument Lambda functions. The function must take the document to be indexed and emit either a single scalar value or an array of scalar values.

```javascript
client.query({
  binding1: q.Query(
    q.Lambda('document', q.Select(['data', 'field'], q.Var('document')))
  ),
})
.then((ret) => console.log(ret))
```

```
{ binding1:
   Query(Lambda("document", Select(["data", "field"], Var("document")))) }
```

### Term Objects

Term objects describe the fields whose values are used to search for entries in the index.

The following example demonstrates an index’s `terms` field definition with two term objects, the first specifies a binding, the second specifies a document field:

```javascript
client.query({
  terms: [
    { binding: 'binding1' },
    { field: ['data', 'field'] },
  ],
})
.then((ret) => console.log(ret))
```

```
{ terms: [ { binding: 'binding1' }, { field: [Array] } ] }
```

### Value Objects

Value objects describe the fields whose values should be used to sort the index, and whose values should be reported in query results.

The following example demonstrates an index’s `values` field definition with two term objects, the first specifies a binding, the second specifies a document field that should be sorted in reverse:

```javascript
client.query({
  values: [
    { binding: 'binding1' },
    { field: ['data', 'field'], reverse: true },
  ],
})
.then((ret) => console.log(ret))
```

```
{ values:
   [ { binding: 'binding1' }, { field: [Array], reverse: true } ] }
```

# Functions

FQL provides many built-in functions that can be used to query and modify a database. Functions, also known as user-defined functions (UDFs), provide a mechanism to store and run commonly used FaunaDB queries. FaunaDB supports two different types of functions:
* ***Built-in functions***: Building blocks to query or mutate FaunaDB databases.
* ***User-defined functions***: Combines functions, built-in or user-defined, into queries that can be executed repeatedly.

UDFs can be anonymous, when declared with the `Lambda` function, or can be named by using `CreateFunction`. A simple query that uses a built-in function could be:

```shell
Add(1, 1)
```

Suppose that we want to add 1 to several numbers. We could use an anonymous function:

```shell
Map(
  [ 1, 2, 3, 4, 5 ],
  Lambda(
    "number",
    Add(1, Var("number"))
  )
)
```

That query executes the anonymous Lambda function once per entry in the array that `Map` processes. For more complex functions, where it might be unwieldy to include the function itself in each query that needs to use it, we can create a named function:

```shell
CreateFunction({
  name: "increment",
  body: Query(Lambda("number", Add(1, Var("number"))))
})
```

Now that the function has been stored and has a name, we can run a query that executes our function like this:

```shell
Call(Function("increment"), 50)
```

### Schema for Named Functions

UDFs are documents that exist within internal "functions" collection of FaunaDB, which can be referred to by name using the built-in `Function` function. Each function document is stored within the context of the enclosing database: peer, parent, and child databases store functions independently.

|Field|Type|Definition and Requirements|
|-----|----|---------------------------|
|`name`|String|The name of the function. Cannot be `events`, `sets`, `self`, `documents`, or `_`.|
|`body`|Query|The query to be run when the function is executed. Must be wrapped in a `Query` function.|
|`role`|String|Optional- When the function is executed, it should be granted the privileges of the specified `role`. Can be one of `admin`, `server`, `server-readonly`, or `client`.|
|`data`|Object|Optional - A JSON object that can be used to store metadata about a function.|

### Signature

The signature of a UDF takes two parameters:
* The ***parameter list*** specifies the name(s) of the parameters passed to the function upon execution. The parameter list could be a single String name, or an array of string names.
* The ***query expression*** is any valid FQL query. To use named parameters within the query expression, use the `Var` function.

### Permissions

By default, UDFs are executed with the privileges of the current query session. For example, if your client code connects to FaunaDB using a "client" key, any called UDFs would, by default, execute with "client" privileges. You can specify a `role` for named UDFs, which grants the functions of the named role while the UDF executes. 

# Sets

Sets are sorted groups of tuples. An index derives sets from documents within the collections in its source. As documents are created, modified, and deleted, sets are updated to reflect their documents' current state.

Indexes are groups of sets, each of which has a natural key; a tuple of zero or more ***terms***. The `Match` query function constructs a set ref to identify a set for a given tuple of terms within an index:

```javascript
client.query(q.Match(q.Index('spells_by_element'), 'water'))
.then((ret) => console.log(ret))
```

```
SetRef({"match":{"@ref":{"id":"spells_by_element","class":{"@ref":{"id":"indexes"}}}},"terms":"water"})
```

Set refs are unique according to their structure: Two set refs with the same structure refer to the same set within a database. Query functions such as `Union`, `Intersection`, and `Join` allow the construction of more complex logical set identifiers:

```javascript
client.query(
  q.Intersection(
    q.Match(q.Index('spells_by_element'), 'water'),
    q.Match(q.Index('spells_by_element'), 'fire'),
  )
)
.then((ret) => console.log(ret))
```

```
SetRef({"intersection":[{"@set":{"match":{"@ref":{"id":"spells_by_element","class":{"@ref":{"id":"indexes"}}}},"terms":"water"}},{"@set":{"match":{"@ref":{"id":"spells_by_element","class":{"@ref":{"id":"indexes"}}}},"terms":"fire"}}]})
```
