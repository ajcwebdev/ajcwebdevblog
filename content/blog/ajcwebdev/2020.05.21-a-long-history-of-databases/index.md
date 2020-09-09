---
title: a long history of databases
date: "2020-05-21"
description: database managament systems, data models, and query languages
---

> There are no widely accepted definitions for the terms data-base systems or information systems.  
> -Senko, Altman, Astrahan, Fehder, [Data Structures and Accessing in Data-Base Systems (1973)](pdfs.semanticscholar.org/2959/c28a3e5a5fc0d54a5acaa848f738a74a9724.pdf)

## Database Management Systems

A general-purpose DBMS is designed to allow the definition, creation, querying, update, and administration of databases.

> Database management has two main functions. First is the inquiry or retrieval activity that reaccesses previously stored data in order to determine the recorded status of some real world entity or relationship. The second activity of database management is to update, which includes the original storage of data, its repeated modification as things change, and ultimately, its deletion from the system when the data is no longer needed.  
> -Charles W. Bachman, [The Programmer as Navigator (November 1973)](dl.acm.org/doi/pdf/10.1145/355611.362534)

### Information Management System

IBM designed IMS with Rockwell and Caterpillar in 1966 for the Apollo program. It was used to inventory very large bill of materials for the Saturn V moon rocket and Apollo space vehicle. IMS stored data using a hierarchical model unlike the relational model that would gain popularity in the 1970s. The push and pull between relational vs. hierarchical models will be a recurring theme throughout this history.

> Future users of large data banks must be protected from having to know how the data is organized in the machine (the internal representation).  
> -E. F. Codd, [A Relational Model of Data for Large Shared Data Banks (June 1970)](https://dl.acm.org/doi/pdf/10.1145/362384.362685)

### Ingres

Ingres (Interactive Graphics and Retrieval System) began as a research project at the University of California, Berkeley, in the early 1970s. Like many other Berkeley projects it was available under a version of the BSD license. In 1973, Stonebraker and his colleague Eugene Wong started researching relational database systems after reading E. F. Codd's papers on the relational data model.

> The principal components of INGRES include: the query language QUEL, an algorithm for processing interactions based on the principle of "decomposition," the access methods supported, and an approach to access control, views, and integrity preservation via query modification.
> -Held, Stonebraker, Wong, [INGRES: A Relational Data Base System (1975)](https://dl.acm.org/doi/pdf/10.1145/1499949.1500029)

### System R

IBM System R was the first implementation of SQL. It started as a research project at the San Jose Research Laboratory in 1974.

## Models

A **data model** is a collection of concepts for describing the data in a database. A **schema** is a description of a particular collection of data, using a given data model.

### Heirarchical

### Network

### Relational

> The relational model is often described as having the following three aspects:  
> * **Structural**: The data in the database is perceived by the user as tables, and
nothing but tables.  
> * **Integrity**: Those tables satisfy certain integrity constraints.  
> * **Manipulative**: The operators available to the user for manipulating those
tables derive tables from tables.  
> -Christopher J. Date, [(An Introduction to Database Systems (1975))](http://ce.sharif.edu/courses/84-85/1/ce384/resources/root/C.%20J.%20Date/ch3%20of%20date.pdf)

#### Entity-Relationship Model

> The entity-relationship model adopts the more natural view that the real world consists of entities and relationships. It incorporates some of the important semantic information about the real world.  
> -Peter Pin-Shan Chen, [The Entity-Relationship Model: Toward a Unified View of Data (1976)](https://dl.acm.org/doi/pdf/10.1145/320434.320440)

### Key-Value/Document

### Graph

## Query Languages

> In the near future we can expect a great variety of languages to be proposed for interrogating and updating data bases. When the computation-oriented components of such a language are removed, we refer to the remaining storage and retrieval oriented sublanguage as a data sublanguaqe. A data sublanguage may be stand-alone -- in which case, it is commonly called a query language.  
> -E. F. Codd, [Relational Completeness of Data Base Sublanguages (March 1972)](http://www.inf.unibz.it/~franconi/teaching/2006/kbdb/Codd72a.pdf)

### SEQUEL

Chamberlin, Boyce - [SEQUEL: A Structured English Query Language (1974)](https://researcher.watson.ibm.com/researcher/files/us-dchamber/sequel-1974.pdf)

### QUEL

### SQL


### Transactions

> A transaction is a transformation of state which has the properties of atomicity (all or nothing), durability (effects survive failures) and consistency (a correet transformation). The transaction concept is key to the structuring of data management applications.  
> -Jim Gray, [The Transaction Concept: Virtues and Limitations (June 1981)](https://jimgray.azurewebsites.net/papers/theTransactionConcept.pdf)