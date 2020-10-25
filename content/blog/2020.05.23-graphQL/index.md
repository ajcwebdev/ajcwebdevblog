---
title: graphQL
date: "2020-05-23"
description: a history of competing API specifications
---

*GraphQL is unapologetically driven by the requirements of views and the front-end engineers that write them. We start with their way of thinking and requirements and build the language and runtime necessary to enable that.*  
***Nick Schrock - [GraphQL Introduction (May 1, 2015)](https://reactjs.org/blog/2015/05/01/graphql-introduction.html)***

GraphQL is a query language for APIs. It was created by Facebook for data fetching in their mobile application.

[![Image](https://sedaily-topics.s3.amazonaws.com/topic_images/0_7311834466847915.jpg)](https://graphql.org/)

GraphQL is frequently compared to REST, the dominant paradigm for client-server communication. To understand GraphQL it is useful to first understand REST and how GraphQL differs. But to understand REST it is useful to first understand APIs. WTF is an API? APIs are how computers talk to each other.

*I would like to rather think of us as the API community not as the GraphQL community or REST API community. We are one community and we should work together to deliver good technology to mankind.*  
***Zdenek “Z” Nemec - [REST vs. GraphQL: Critical Look (November 2, 2018)](https://www.youtube.com/watch?v=yLf0rIaRtRc)***

### Representational state transfer

*REST is simple. There is only one person in the world who does REST. It’s the guy who invented it. Nobody else does.*  
***Joe Eames - [JSON APIs (January 10, 2014)](https://devchat.tv/js-jabber/091-jsj-json-apis/)***

*The design rationale behind the Web architecture can be described by an architectural style consisting of the set of constraints applied to elements within the architecture. By examining the impact of each constraint as it is added to the evolving style, we can identify the properties induced by the Web's constraints. Additional constraints can then be applied to form a new architectural style that better reflects the desired properties of a modern Web architecture.*  
***Roy Fielding - [Architectural Styles and the Design of Network-based Software Architectures (2000)](https://www.ics.uci.edu/~fielding/pubs/dissertation/fielding_dissertation.pdf)***

[![Image](https://sedaily-topics.s3.amazonaws.com/topic_images/0_6740655432542186.jpg)](https://medium.com/@sagar.mane006/understanding-rest-representational-state-transfer-85256b9424aa)

Philosophical discussions aside, REST is:  
POST - Create  
GET - Read - Retrieve  
PUT - Update  
DELETE - Destroy  

REST is CRUD. CRUD stands for create, read, update, delete. All programmers need to be familiar with this terminology.

Astute readers may be wondering why we need 9 terms to describe 4 concepts, to which I do not have a good answer. The term seems to originate from  James Martin's [Managing the Data-base Environment](http://is.cba.edu.kw/433/Handouts/ch01.pdf) in 1983.

### Simple Object Access Protocol

Despite the widespread comparison to REST, GraphQL is closer in design to a lesser known protocol created in 1999 called [SOAP](https://tools.ietf.org/html/draft-box-http-soap-00) that failed to gain widespread adoption in comparison to REST.

SOAP used XML as its message format. XML was designed to be a subset of SGML, and both competed against HTML to become the underlying technology of the World Wide Web. HTML ultimately won out with JSON emerging as a modern attempt at improving on XML.

[![Image](https://sedaily-topics.s3.amazonaws.com/topic_images/0_4572209629373618.jpg)](https://graphql.org/)

## Client Side 

#### Relay

*Relay is a new framework from Facebook that provides data-fetching functionality for React applications. Each component specifies its own data dependencies declaratively using a query language called GraphQL.*

*The data is made available to the component via properties on `this.props`. Developers compose these React components naturally, and Relay takes care of composing the data queries into efficient batches.*  
***Greg Hurrell - [Introducing Relay and GraphQL (February 20, 2015)](https://reactjs.org/blog/2015/02/20/introducing-relay-and-graphql.html)***

#### Apollo

Apollo is a platform for building a data graph, a communication layer that seamlessly connects your application clients (such as React and iOS apps) to your back-end services. Apollo can be adopted incrementally, meaning you can set it up alongside an existing solution (such as a REST API) and migrate functionality at your convenience.

![Apollo-server-architecture](https://www.apollographql.com/docs/apollo-server/ee7fbac9c0ca5b1dd6aef886bb695e63/index-diagram.svg)

Apollo uses GraphQL because it believes it's straightforward to add new types and fields to your API, and similarly straightforward for your clients to begin using those fields. This helps designing, developing, and deploying features quickly. The Apollo platform along with GraphQL handles considerations like caching, data normalization, and optimistic UI rendering.

## Server Side

#### Hasura

Hasura is an open source engine that connects to your databases & microservices and auto-generates a production-ready GraphQL backend. The Hasura GraphQL engine sets up a GraphQL server and triggers events over a Postgres database.

To use the Hasura GraphQL engine, you need to:

1. Run the Hasura GraphQL engine with access to a Postgres database
2. Use the Hasura console (an admin UI) that connects to the Hasura GraphQL engine to help you build your schema and run GraphQL queries

![Image](https://sedaily-topics.s3.amazonaws.com/topic_images/0_5560332280141722.jpg)

#### Prisma

Prisma is a query builder that replaces traditional ORMs and can be used to build GraphQL servers, REST APIs, and microservices. Prisma originally focused heavily on GraphQL but with their 2.0 release that seems to have changed.

Here's the Prisma [docs explanation](https://www.prisma.io/blog/graphql-schema-stitching-explained-schema-delegation-4c6caf468405) of the shifting relationship between Prisma and GraphQL:

*GraphQL [schema delegation](https://www.prisma.io/blog/graphql-schema-stitching-explained-schema-delegation-4c6caf468405/) connects two GraphQL schemas by passing the info object from a resolver of the first GraphQL schema to a resolver of the second GraphQL schema. Schema delegation also is the foundation for [GraphQL binding](https://github.com/graphql-binding/graphql-binding).*

*Prisma 1 officially supports both schema delegation and GraphQL binding as it exposes a GraphQL CRUD API through the [Prisma server](https://www.prisma.io/docs/prisma-server/).This API can be used to as the foundation for an application-layer GraphQL API created with GraphQL binding.*

*With Prisma 2.0, Prisma's [query engine](https://www.prisma.io/docs/reference/tools-and-interfaces/prisma-client/query-engine/) doesn't expose a [spec](https://graphql.github.io/graphql-spec/June2018/)-compliant GraphQL endpoint any more, so usage of schema delegation and GraphQL binding with Prisma 2.0 is not supported. To build GraphQL servers with Prisma 2.0, be sure to check out [GraphQL Nexus](https://nexusjs.org/). GraphQL Nexus provides a code-first and type-safe way to build GraphQL servers in a scalable way.*

#### Nexus

Nexus provides declarative, code-first GraphQL schemas for JavaScript/TypeScript with robust, composable type definitions. It has an ambiguous relation to Prisma and was announced on their blog in 2019 by Tim Griesser, an engineer at Cypress.io. [There is a very, very long post in the Prisma docs called Old to new Nexus](https://www.prisma.io/docs/guides/upgrade-from-prisma-1/upgrading-nexus-prisma-to-nexus).

The Nexus framework is built on top of the [Nexus Schema library built by Tim Griesser](https://github.com/graphql-nexus/schema). 

### GitHub, Gatsby, Netlify

*GraphQL becomes the one and only mediator between your frontend and your backend.*  
***Tom Preston-Werner - [RedwoodJS with Tom Preston-Werner](https://www.softwaredaily.com/post/5ec7997912b353000c6381d8/RedwoodJS-with-Tom-PrestonWerner)***

GitHub began supporting GraphQL in [2016](https://github.blog/2016-09-14-the-github-graphql-api/) which sent a strong signal that the specification was ready for primetime. That same year Chris Biscardi inspired Kyle Matthews to rewrite Gatsby with GraphQL as a core architectural pillar and Netlify also began [promoting](https://www.netlify.com/blog/2016/11/30/graphql-at-github/) [GraphQL](https://www.netlify.com/blog/2016/12/20/try-out-graphql/).

Together these projects launched the JAMstack movement (JavaScript, APIs, Markdown), an evolution of the static site generation paradigm popularized by Jekyll and Hugo. GraphQL is the A in the JAM.

*GraphQL's design enables clients where smaller payload sizes are essential. For example, a mobile app could simplify its requests by only asking for the data it needs. This enables new possibilities and workflows that are freed from the limitations of downloading and parsing massive JSON blobs.*  
***GitHub Engineering - [The GitHub GraphQL API (September 14, 2016)](https://github.blog/2016-09-14-the-github-graphql-api/)***

### RedwoodJS

[![Image](https://sedaily-topics.s3.amazonaws.com/topic_images/0_04340078035076256.png)](https://www.netlify.com/blog/2020/03/11/redwoodjs-the-full-stack-jamstack-framework/)

Redwood can deploy your GraphQL API to a Lambda function. This is not appropriate for all use cases, but on hosting providers like Netlify, it makes deployment a breeze. As time goes on, "functions" will continue to enjoy performance improvements which will further increase the number of use cases that can take advantage of this technology.

Databases are a little trickier, especially the traditional relational ones like PostgreSQL and MySQL. Right now, you still need to set these up manually, but we are working hard with Netlify and other providers to fulfill the serverless dream here too.

Redwood is intentionally pushing the boundaries of what's possible with JAMstack. In fact, the whole reason Tom started working on Redwood is because of a tweet he posted some time ago:

*Prediction: within 5 years, you’ll build your next large scale, fully featured web app with #JAMstack and deploy on @Netlify.*  
***—@mojombo • 9 July 2018***

## Who is using GraphQL?

GraphQL is used by teams of all sizes in many different environments and languages to power mobile apps, websites, and APIs. According to the [Who is using GraphQL?](https://graphql.org/users/) page on [graphql.org](https://graphql.org/) there are currently 87 adoptees of GraphQL including:

Airbnb, Atlassian, Braintree, Facebook (duh), GitHub, Intuit, SAP, Lyft, NBCUniversal, New Relic, PayPal, Pinterest, Pluralsight, Rakuten, Shopify, Starbucks, The New York Times, Twitter, Wayfair, and Yelp.

The combined market cap of this list of 20 companies not including the remaining 67 exceeds three trillion dollars.

[![Image](https://sedaily-topics.s3.amazonaws.com/topic_images/0_599380641317443.jpg)](https://www.youtube.com/watch?v=7wzR4Ig5pTI)

# Videos

[Learn GraphQL In 40 Minutes](https://www.youtube.com/watch?v=ZQL7tL2S0oQ) - Web Dev Simplified

[GraphQL Tutorial](https://www.youtube.com/watch?v=Y0lDGjwRYKw) - The Net Ninja

[What Is GraphQL?](https://www.youtube.com/watch?v=VjXb3PRL9WI) - LevelUpTuts

[Building a GraphQL Server](https://www.youtube.com/watch?v=PEcJxkylcRM) - Traversy Media