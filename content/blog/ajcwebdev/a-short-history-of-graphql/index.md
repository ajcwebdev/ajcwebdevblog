---
title: a short history of GraphQL
date: "2020-05-23"
description: A history of competing API specifications.
---

*GraphQL is unapologetically driven by the requirements of views and the front-end engineers that write them. We start with their way of thinking and requirements and build the language and runtime necessary to enable that.  
-Nick Schrock, [GraphQL Introduction (May 1, 2015)](https://reactjs.org/blog/2015/05/01/graphql-introduction.html)*

GraphQL is a query language for APIs. It was created by Facebook for data fetching in their mobile application.

[![Image](https://sedaily-topics.s3.amazonaws.com/topic_images/0_7311834466847915.jpg)](https://graphql.org/)

GraphQL is frequently compared to REST, the dominant paradigm for client-server communication. To understand GraphQL it is useful to first understand REST and how GraphQL differs. But to understand REST it is useful to first understand APIs. WTF is an API? APIs are how computers talk to each other.

*I would like to rather think of us as the API community not as the GraphQL community or REST API community. We are one community and we should work together to deliver good technology to mankind.
-Zdenek “Z” Nemec, [REST vs. GraphQL: Critical Look (November 2, 2018)](https://www.youtube.com/watch?v=yLf0rIaRtRc)*

### Representational state transfer

*REST is simple. There is only one person in the world who does REST. It’s the guy who invented it. Nobody else does.  
-Joe Eames, [JSON APIs (January 10, 2014)](https://devchat.tv/js-jabber/091-jsj-json-apis/)*

*The design rationale behind the Web architecture can be described by an architectural style consisting of the set of constraints applied to elements within the architecture. By examining the impact of each constraint as it is added to the evolving style, we can identify the properties induced by the Web's constraints. Additional constraints can then be applied to form a new architectural style that better reflects the desired properties of a modern Web architecture.  
-Roy Fielding, [Architectural Styles and the Design of Network-based Software Architectures (2000)](https://www.ics.uci.edu/~fielding/pubs/dissertation/fielding_dissertation.pdf)*

[![Image](https://sedaily-topics.s3.amazonaws.com/topic_images/0_6740655432542186.jpg)](https://medium.com/@sagar.mane006/understanding-rest-representational-state-transfer-85256b9424aa)

Philosophical discussions aside, REST is:
GET - Read
POST - Create
PUT - Update
DELETE - Delete

REST is CRUD. CRUD stands for create, read, update, delete. All programmers need to be familiar with this terminology. Astute readers may be wondering why we need 7 terms to describe 4 concepts, to which I do not have a good answer.

### Simple Object Access Protocol

Despite the widespread comparison to REST, GraphQL is closer in design to a lesser known protocol created in 1999 called [SOAP](https://tools.ietf.org/html/draft-box-http-soap-00) that failed to gain widespread adoption in comparison to REST. SOAP used XML as its message format. XML was designed to be a subset of SGML, and both competed against HTML to become the underlying technology of the World Wide Web. HTML ultimately won out with JSON emerging as a modern attempt at improving on XML.

[![Image](https://sedaily-topics.s3.amazonaws.com/topic_images/0_4572209629373618.jpg)](https://graphql.org/)

### Client Side: Relay and Apollo

*Relay is a new framework from Facebook that provides data-fetching functionality for React applications. Each component specifies its own data dependencies declaratively using a query language called GraphQL. The data is made available to the component via properties on this.props. Developers compose these React components naturally, and Relay takes care of composing the data queries into efficient batches.  
-Greg Hurrell, [Introducing Relay and GraphQL (February 20, 2015)](https://reactjs.org/blog/2015/02/20/introducing-relay-and-graphql.html)*

*Apollo is a platform for building a data graph, a communication layer that seamlessly connects your application clients (such as React and iOS apps) to your back-end services.  
-[Apollo Documentation](https://www.apollographql.com/docs/)*

### Server Side: Prisma and Hasura

The Hasura GraphQL engine sets up a GraphQL server and triggers events over a Postgres database. Prisma replaces traditional ORMs and can be used to build GraphQL servers, REST APIs, and microservices.

### GitHub, Gatsby, Netlify

*GraphQL becomes the one and only mediator between your frontend and your backend.  
-Tom Preston-Werner*

GitHub began supporting GraphQL in [2016](https://github.blog/2016-09-14-the-github-graphql-api/) which sent a strong signal that the specification was ready for primetime. That same year Chris Biscardi inspired Kyle Matthews to rewrite Gatsby with GraphQL as a core architectural pillar and Netlify also began [promoting](https://www.netlify.com/blog/2016/11/30/graphql-at-github/) [GraphQL](https://www.netlify.com/blog/2016/12/20/try-out-graphql/). Together these projects launched the JAMstack movement (JavaScript, APIs, Markdown), an evolution of the static site generation paradigm popularized by Jekyll and Hugo. GraphQL is the A in the JAM.

*GraphQL's design enables clients where smaller payload sizes are essential. For example, a mobile app could simplify its requests by only asking for the data it needs. This enables new possibilities and workflows that are freed from the limitations of downloading and parsing massive JSON blobs.  
-GitHub Engineering, [The GitHub GraphQL API (September 14, 2016)](https://github.blog/2016-09-14-the-github-graphql-api/)*

### RedwoodJS

[![Image](https://sedaily-topics.s3.amazonaws.com/topic_images/0_04340078035076256.png)](https://www.netlify.com/blog/2020/03/11/redwoodjs-the-full-stack-jamstack-framework/)