---
title: redwoodjs and faunadb
date: "2020-08-13"
description: together at last
---

# FaunaDB and why it fits well with RedwoodJS

## Introduction

* RedwoodJS
  - Fullstack
  - Jamstack

* FaunaDB
  - Serverless

* Create Redwood App
  - Home Page
  - HomePageCell

* Redwood Directory Structure

## Fauna Database

* Create FaunaDB account

* Create new Database
  - Give database a name
  - Model our data with GraphQL schema
  - Import and seed data to Fauna

* Create database key
  - Add key to Redwood config vars

* Test data with GraphiQL playground

# Introduction

## RedwoodJS

RedwoodJS is an opinionated, full-stack, serverless web application framework for building and deploying JAMstack applications. It was created by Tom-Preston Werner and combines a variety of technologies and techniques that have been influencing the industry over the last 5-10 years. This includes:
* React frontend
* Statically delivered files served from a CDN
* GraphQL to connect your frontend and backend
* AWS Lambdas for serverless deployment
* Deployable with a single `git push` command

>*My dream of a future is for something I call a universal deployment machine, which means I write my code. It's all text, I just write text. Then I commit to GitHub. Then it's picked up and it's deployed into reality. That's it, that's the whole thing.*
>
>***Tom Preston Warner***  
>***[RedwoodJS Shoptalk (May 11, 2020)](https://shoptalkshow.com/412/)***

## Fullstack

A long running emphasis throughout the history of React has been its identification as a library instead of a framework. The one-liner for React has always been ***a JavaScript library for building user interfaces***.

Since React did not seek to provide strong conventions many different groups started building their own custom solutions on top of React. This resulted in an explosion of new frameworks, build tools, state management libraries, and styling techniques. All this innovation has been incredible, but it's made building apps with React increasingly complicated.

## Jamstack

In 2008, Tom Preston-Werner published a blog post titled “Blogging Like a Hacker,” which told his story of blogging, programming, and his eventual invention of Jekyll. He decided to approach blogging from a software developers perspective by storing his writing in a Git repository and publishing via a deploy script or post-commit hook.

Jekyll works by:
1. Taking a template directory representing the raw form of a website
2. Running it through Textile and Liquid converters
3. Spiting out a complete, static website
4. Serving with Apache or similar web server

In 2014, Mathias Biilmann Christensen created [staticgen.com](http://mathias-biilmann.net/posts/2014/07/01/staticgen), a leaderboard of top open-source static site generators. Mathias was inspired by the Git-centered workflow and static site generation Jekyll enabled. He wanted to build a company to help developers easily deploy their code and co-founded Netlify with his childhood friend Christian Bach in December 2014. Tom Preston-Werner was an early investor in Netlify.

The next year Gatsby was created by Kyle Mathews. It started as a static site generator built with React, but as the project grew it no longer functioned as simply a static site generator and Kyle found the term to be ill fitting to the project.

Gatsby incorporated GraphQL and used 3rd party APIs to perform various dynamic tasks that could not be achieved with older static site generators. Other projects appeared that were influenced by this architecture including [Gridsome](https://gridsome.org/) and [Scully](https://www.netlify.com/blog/2019/12/16/introducing-scully-the-angular-static-site-generator/).

This started to be referred to as the [JAMstack](https://jamstack.org/), as in JavaScript, APIs, and Markup. Mathias credits [Andreas Sæbjørnsen](https://changelog.com/podcast/251) with first coining the term.

## FaunaDB

FaunaDB is a serverless global database designed for low latency and developer productivity. It has proved particularly appealing to Jamstack developers for its global scaleability, native GraphQL API, and FQL query language.

>*Being a serverless distributed database, the JAMstack world is a natural fit for our system, but long before we were chasing JAMstack developers, we were using the stack ourselves.*
>
>***Matt Attaway***  
>***[Lessons Learned Livin' La Vida JAMstack (January 24, 2020)](https://fauna.com/blog/lessons-learned-livin-la-vida-jamstack)***

### Serverless

***Serverless*** is commonly used to refer to Function-as-a-Service cloud products like AWS Lambda. Instead of paying for a server to always be running and ready to accept requests, you pay based on the specific number of function calls your app invokes.

## Create Redwood App

To start we'll create a new Redwood app from scratch with the Redwood CLI. If you don't have yarn installed enter the following command:

```
yarn install
```

Now we'll use `yarn create redwood-app` to generate the basic structure of our app. 

```
yarn create redwood-app ./redwood-fauna
```

I've called my project `redwood-fauna` but feel free to select whatever name you want for your application. We'll now `cd` into our new project and use `yarn rw dev` to start our development server.

```
cd redwood-fauna
yarn rw dev
```

Our project's frontend is running on `localhost:8910` and our backend is running on `localhost:8911` ready to receive GraphQL queries.

![](https://res.cloudinary.com/practicaldev/image/fetch/s--yyS441iU--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_880/https://dev-to-uploads.s3.amazonaws.com/i/ycisyl2bbxasa9j6zr9b.jpg)

## Redwood Directory Structure

One of Redwood's guiding philosophies is that there is power in standards, so it makes decisions for you about which technologies to use, how to organize your code into files, and how to name things.

It can be a little overwhelming to look at everything that's already been generated for us. The first thing to pay attention to is that Redwood apps are separated into two directories:
* `api` for backend
* `web` for frontend

```
├── api
│   ├── prisma
│   │   ├── schema.prisma
│   │   └── seeds.js
│   └── src
│       ├── functions
│       │   └── graphql.js
│       ├── graphql
│       ├── lib
│       │   └── db.js
│       └── services
└── web
    ├── public
    │   ├── favicon.png
    │   ├── README.md
    │   └── robots.txt
    └── src
        ├── components
        ├── layouts
        ├── pages
            ├── FatalErrorPage
            │   └── FatalErrorPage.js
            └── NotFoundPage
                └── NotFoundPage.js
        ├── index.css
        ├── index.html
        ├── index.js
        └── Routes.js
```

Each side has their own path in the codebase. These are managed by Yarn [workspaces](https://classic.yarnpkg.com/en/docs/workspaces/). We will be talking to the Fauna client directly so we can delete the `prisma` directory along with the files inside it and we can delete the code in the `db.js`.

With our application now set up we can start creating pages. We'll use the `generate page` command to create a home page and a folder to hold that page. Instead of `generate` we can use `g` to save some typing.

```
yarn rw g page home /
```

# Fauna Database

## Create FaunaDB account

You'll need a FaunaDB account to follow along but it's free for creating simple low traffic databases. You can use your email to create an account or either your Github or Netlify account. FaunaDB Shell does not currently support GitHub or Netlify logins so using those will add a couple extra steps when we want to authenticate with the fauna-shell.

First we need to install the `faunadb` client and the `fauna-shell` which will let easily work with our database.

```
npm install --save faunadb
npm install -g fauna-shell
```

Now we'll login to our Fauna account so we can access a database with the shell.

```
fauna cloud-login
```

You'll be asked to verify your email and password. If you signed up for FaunaDB using your GitHub or Netlify credentials, follow [these steps](https://docs.fauna.com/fauna/current/start/cloud-github), then continue with [Start using your database](https://docs.fauna.com/fauna/current/start/cloud#shell).

## Create new Database

To create your database enter the `fauna create-database` command and give your database a name.

```
fauna create-database my_db
```

To start the fauna shell with our new database we'll use `fauna shell` and the name of the database.

```
fauna shell my_db
```

To test out our database we'll create a collection with the name `posts`.

```javascript
CreateColletion({ name: "posts" })
```

After entering this command you'll receive the following output:

```javascript
{
  ref: Collection("posts"),
  ts: 1597179021386000,
  history_days: 30,
  name: 'posts'
}
```

Now we'll create an index for retrieving our posts.

```javascript
CreateIndex({
  name: "posts_by_title",
  source: Collection("posts"),
  terms: [{ field: ["data", "title"] }]
})
```

You'll then receive the index instance as a response

```javascript
{ ref: Index("posts_by_title"),
  ts: 1533753979163761,
  active: true,
  partitions: 1,
  name: "posts_by_title",
  source: Collection("posts"),
  terms: [ { field: [ "data", "title" ] } ] }
```

## Model our data with GraphQL schema

In our `graphql` directory we'll create a `posts.sdl.js` file and enter the following code:

```javascript
import gql from 'graphql-tag'

export const schema = gql`
  type Post {
    title: String!
  }

  type Query {
    posts: [Post!]!
    post(id: Int!): Post!
  }
`
```

## Import and seed data to Fauna

Let's create our first blog post:

```javascript
Create(
  Collection("posts"),
  { data: { title: "Deno is a secure runtime for JavaScript and TypeScript" } }
)
```

You'll receive the following output:

```javascript
{ ref: Ref(Collection("posts"), "207089183860195845"),
  ts: 1533754485757944,
  data: { title: "Deno is a secure runtime for JavaScript and TypeScript" } }
```

We can create multiple blog posts with the `Map` function:

```javascript
Map(
  [
    "YugabyteDB is an open source, high-performance, distributed SQL database for global, internet-scale apps",
    "NextJS is a React framework for building production grade applications that scale"
  ],
  Lambda("post_title",
    Create(
      Collection("posts"), { data: { title: Var("post_title") } }
    )
  )
)
```

We are calling `Map` with an array of posts and a `Lambda` that takes `"post_title"` as it's only parameter. `"post_title"` is then used inside the Lambda to provide the `title` field for each new post.

```javascript
[ { ref: Ref(Collection("posts"), "207089200754854408"),
    ts: 1533754501878440,
    data: { title: "Deno is a secure runtime for JavaScript and TypeScript" } },
  { ref: Ref(Collection("posts"), "207089200754853384"),
    ts: 1533754501878440,
    data: { title: "YugabyteDB is an open source, high-performance, distributed SQL database for global, internet-scale apps" } },
  { ref: Ref(Collection("posts"), "207089200754852360"),
    ts: 1533754501878440,
    data: { title: "NextJS is a React framework for building production grade applications that scale" } } ]
```

We can query for a specific post by using its ID.

```javascript
Get(Ref(Collection("posts"), "207089200754852360"))
```

This will give the following output:

```javascript
{ ref: Ref(Collection("posts"), "207089200754852360"),
  ts: 1533754501878440,
  data: { title: "NextJS is a React framework for building production grade applications that scale" } }
```

We could also query with the posts title:

```javascript
Get(
  Match(
    Index("posts_by_title"),
    "Deno is a secure runtime for JavaScript and TypeScript"
  )
)
```

This will give the following output:

```javascript
{ ref: Ref(Collection("posts"), "207089200754854408"),
  ts: 1533754501878440,
  data: { title: "Deno is a secure runtime for JavaScript and TypeScript" } }
```

## Create database key
### Add key to Redwood config vars

## Test data with GraphiQL playground