---
title: nexus
date: "2020-06-20"
description: declarative, code-first graphQL schemas with type definitions
---

Nexus provides declarative, code-first GraphQL schemas for JavaScript/TypeScript with robust, composable type definitions. It has an ambiguous relation to Prisma and was announced on their blog in 2019 by Tim Griesser, an engineer at Cypress.io. [There is a very, very long post in the Prisma docs called Old to new Nexus](https://www.prisma.io/docs/guides/upgrade-from-prisma-1/upgrading-nexus-prisma-to-nexus). The Nexus framework is built on top of the [Nexus Schema library built by Tim Griesser](https://github.com/graphql-nexus/schema). 

## Schema Definition Language

Its SDL converter can turn an existing schema into Nexus code. It aims to combine the simplicity and ease of development of SDL development approaches like [graphql-tools](https://www.graphql-tools.com/docs/introduction/) with the long-term maintainability of programmatic construction as seen in:
* [graphene-python](https://docs.graphene-python.org/en/latest/)
* [graphql-ruby](https://github.com/rmosolgo/graphql-ruby)
* [graphql-js](https://github.com/graphql/graphql-js)

The project seems to have two separate websites with different documentation containing different styling and content:
* [nexus.js.org](https://nexus.js.org/docs/getting-started)
* [nexusjs.org](https://www.nexusjs.org/#/README)

Since the primary purpose of documentation is to provide clarification and a source of truth to developers it would probably be in the project's best interest to consolidate to a single domain. Until told otherwise I'll be taking info from both. If that doesn't sounds like a good idea then you understand why there should be one site.

### Type-Safe by Default

GraphQL Nexus' APIs were designed with type-safety in mind. Type-definitions are auto-generated as you develop, and inferred in your code.

* IDE completion
* Type error catching
* Automatic Type Inference
* Autocompletion on Type Names

### Works With The Ecosystem

Works with existing graphql-js types when constructing its schema. Generated schema works with:

* Apollo Server
* GraphQL middleware

### Data-Agnostic

Declarative syntax layered on the graphql-js library. Whatever can be done with graphql-js or apollo-tools can be done with Nexus.

## References

#### [The Problems of "Schema-First" GraphQL Server Development](https://www.prisma.io/blog/the-problems-of-schema-first-graphql-development-x1mn4cb0tyl3)
##### Nikolas Burk - January 31, 2019

#### [Introducing GraphQL Nexus: Code-First GraphQL Server Development](https://www.prisma.io/blog/introducing-graphql-nexus-code-first-graphql-server-development-ll6s1yy5cxl5)
##### Tim Griesser - February 7, 2019

#### [Using GraphQL Nexus with a Database](https://www.prisma.io/blog/using-graphql-nexus-with-a-database-pmyl3660ncst)
##### Nikolas Burk - February 12, 2019

#### [SDL as an Artifact: Code First Schemas in TS:JS](https://www.youtube.com/watch?v=DlF226AEYSM)
##### Tim Griesser - November 6, 2019