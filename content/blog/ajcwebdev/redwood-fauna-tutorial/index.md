# Building a Minimum Viable Stack with RedwoodJS and FaunaDB

Hey everyone, I've been working on this tutorial over the last week and it's about 95% done, right now we're getting an error message from our `posts.js` service saying our `db` variable is undefined. Normally this is our PrismaClient but we are connecting to the Fauna Client directly.

I was not the least bit surprised to see that I messed this part up; throughout the entire Redwood tutorial the PrismaClient was always a part of the framework I never had to touch or think about.

Before diving into this I should explain the reasoning behind the way I built the project and structured the tutorial. I knew that just combing these two technologies for the first time would involve a significant degree of complexity, so I wanted to build the simplest possible application and do everything in a way that would cause the least amount of friction.

There is just a single Home route that renders a single HomePage. That page renders a single cell that fetches data with a single GraphQL query. Finally we have a single service for querying the backend and rendering an array of blog titles to the home page.

For writing to our database with create, update, or delete methods we'll use the Fauna Shell and create 3 `posts` that each have a `title`. Redwood will not perform any write operations on the databases. All Redwood is doing is one `GET` request to get an array of `posts`.

## Introduction

* RedwoodJS
* FaunaDB

## Redwood Monorepo

* Create Redwood App
* Redwood Directory Structure
  * Pages
  * Cells
  * GraphQL Serverless Function
  * Schema Definition Language
  * DB
  * Services

## Fauna Database

* Create FaunaDB account
* Create new Database
  * Collections
  * Indexes
  * Create
  * Map
  * Get

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
3. Spitting out a complete, static website
4. Serving with Apache or similar web server

In 2014, Mathias Biilmann Christensen created [staticgen.com](http://mathias-biilmann.net/posts/2014/07/01/staticgen), a leaderboard of top open-source static site generators. Mathias was inspired by the Git-centered workflow and static site generation Jekyll enabled. He wanted to build a company to help developers easily deploy their code and co-founded Netlify with his childhood friend Christian Bach in December 2014. Tom Preston-Werner was an early investor in Netlify.

The next year Gatsby was created by Kyle Mathews. It started as a static site generator built with React, but as the project grew it no longer functioned as simply a static site generator and Kyle found the term to be ill fitting to the project.

Gatsby incorporated GraphQL and used 3rd party APIs to perform various dynamic tasks that could not be achieved with older static site generators. Other projects appeared that were influenced by this architecture including [Gridsome](https://gridsome.org/) and [Scully](https://www.netlify.com/blog/2019/12/16/introducing-scully-the-angular-static-site-generator/).

This started to be referred to as the [JAMstack](https://jamstack.org/), as in JavaScript, APIs, and Markup. Mathias credits [Andreas Sæbjørnsen](https://changelog.com/podcast/251) with first coining the term.

## FaunaDB

FaunaDB is a serverless global database designed for low latency and developer productivity. It has proved particularly appealing to Jamstack developers for its global scalability, native GraphQL API, and FQL query language.

>*Being a serverless distributed database, the JAMstack world is a natural fit for our system, but long before we were chasing JAMstack developers, we were using the stack ourselves.*
>
>***Matt Attaway***  
>***[Lessons Learned Livin' La Vida JAMstack (January 24, 2020)](https://fauna.com/blog/lessons-learned-livin-la-vida-jamstack)***

### Serverless

***Serverless*** is commonly used to refer to Function-as-a-Service cloud products like AWS Lambda. Instead of paying for a server to always be running and ready to accept requests, you pay based on the specific number of function calls your app invokes.

# Redwood Monorepo

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

Each side has their own path in the codebase. These are managed by Yarn [workspaces](https://classic.yarnpkg.com/en/docs/workspaces/). We will be talking to the Fauna client directly so we can delete the `prisma` directory along with the files inside it and we can delete all the code in `db.js`.

## Pages

With our application now set up we can start creating pages. We'll use the `generate page` command to create a home page and a folder to hold that page. Instead of `generate` we can use `g` to save some typing.

```
yarn rw g page home /
```

![](https://dev-to-uploads.s3.amazonaws.com/i/bi7y7f1qd5o1fdi8jhfh.jpg)

If we go to our `web/src/pages` directory we'll see a `HomePage` directory containing this `HomePage.js` file:

```javascript
// web/src/pages/HomePage/HomePage.js

import { Link } from '@redwoodjs/router'

const HomePage = () => {
  return (
    <>
      <h1>HomePage</h1>
      <p>Find me in "./web/src/pages/HomePage/HomePage.js"</p>
      <p>
        My default route is named "home", link to me with `
        <Link to="home">routes.home()</Link>`
      </p>
    </>
  )
}

export default HomePage
```

Let's clean up our component. We'll only have a single route for now so we can delete the `Link` import and `routes.home()`, and we'll delete everything except a single `<h1>` tag.

```javascript
// web/src/pages/HomePage/HomePage.js

const HomePage = () => {
  return (
    <>
      <h1>RedwoodJS+Fauna</h1>
    </>
  )
}

export default HomePage
```

![](https://dev-to-uploads.s3.amazonaws.com/i/yujrc0ic7tewsr1uszic.jpg)

## Cells

Cells provide a simpler and more declarative approach to data fetching. They contain the GraphQL query, loading, empty, error, and success states, each one rendering itself automatically depending on what state your cell is in.

```javascript
// web/src/components/PostsCell/PostsCell.js

export const QUERY = gql`
  query POSTS {
    posts {
      title
    }
  }
`
export const Loading = () => <div>Loading posts...</div>
export const Empty = () => <div>No posts yet!</div>
export const Failure = ({ message }) => <div>Error: {message}</div>
export const Success = ({ posts }) => {
  return (
    <ul>
      { posts.map(post => (
        <li>{post.title}</li>
      ))}
    </ul>
  )
}
```

To render our list of posts we need to import `PostsCell` in our `HomePage.js` file and return the component.

```javascript
// web/src/pages/HomePage/HomePage.js

import PostsCell from 'src/components/PostsCell'

const HomePage = () => {
  return (
    <>
      <h1>RedwoodJS+Fauna</h1>
      <PostsCell />
    </>
  )
}

export default HomePage
```

## GraphQL Serverless Function

Files in `api/src/functions` are serverless functions. Most of `@redwoodjs/api` is for setting up the GraphQL API Redwood Apps come with by default. It happens in essentially four steps:

1. Everything (i.e. sdl and services) is imported
2. The services are wrapped into resolvers
3. The sdl and resolvers are merged/stitched into a schema
4. The ApolloServer is instantiated with said merged/stitched schema and context

```javascript
// api/src/functions/graphql.js

import {
  createGraphQLHandler,
  makeMergedSchema,
  makeServices,
} from '@redwoodjs/api'
import importAll from '@redwoodjs/api/importAll.macro'

import { db } from 'src/lib/db'

const schemas = importAll('api', 'graphql')
const services = importAll('api', 'services')

export const handler = createGraphQLHandler({
  schema: makeMergedSchema({
    schemas,
    services: makeServices({ services }),
  }),
  db,
})
```

## Schema Definition Language

In our `graphql` directory we'll create a `posts.sdl.js`. In this file we'll export a `schema` object containing our GraphQL schema definition language. It is defining a `Post` type which has a `title` that is the type of `String`. It is also defining our `Query` type which will create a `posts` array containing every `Post`.

```javascript
// api/src/graphql/posts.sdl.js

import gql from 'graphql-tag'

export const schema = gql`
  type Post {
    title: String!
  }

  type Query {
    posts: [Post!]!
  }
`
```

## DB

When we generated our project `db` defaulted to an instance of PrismaClient. Since Prisma does not support Fauna at this time we will be using the FaunaDB JavaScript Driver.

```javascript
// api/src/lib/db.js

import faunadb, { query as q } from "faunadb"

export const db = new faunadb.Client({ secret: process.env.FAUNADB_SECRET });
```

## Services

In our services folder we'll create a `posts` folder with a file called `posts.js`. Services are where Redwood centralizes all business logic. These can be used by your GraphQL API or any other place in your backend code.

```javascript
// api/src/services/posts/posts.js

import { db } from 'src/lib/db'

export const posts = () => {
  return db.post.findMany()
}
```

Lets take one more look at our entire directory structure before moving on to the Fauna Shell.

```
├── api
│   └── src
│       ├── functions
│       │   └── graphql.js
│       ├── graphql
│       │   └── posts.sdl.js
│       ├── lib
│       │   └── db.js
│       └── services
│           └── posts
│               └── posts.js
└── web
    ├── public
    │   ├── favicon.png
    │   ├── README.md
    │   └── robots.txt
    └── src
        ├── components
        │   └── PostsCell
        │       └── PostsCell.js
        ├── layouts
        ├── pages
            ├── FatalErrorPage
            ├── HomePage
            │   └── HomePage.js
            └── NotFoundPage
        ├── index.css
        ├── index.html
        ├── index.js
        └── Routes.js
```

# Fauna Database

## Create FaunaDB account

You'll need a FaunaDB account to follow along but it's free for creating simple low traffic databases. You can use your email to create an account or either your Github or Netlify account. FaunaDB Shell does not currently support GitHub or Netlify logins so using those will add a couple extra steps when we want to authenticate with the fauna-shell.

First we need to install the `faunadb` client and the `fauna-shell` which will let us easily work with our database.

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

## Collections

To test out our database we'll create a collection with the name `posts`. A database’s schema is defined by its collections, which are similar to tables in other databases. After entering the command fauna shell will respond with the newly created Collection.

```javascript
CreateCollection({ name: "posts" })
```

```javascript
{
  ref: Collection("posts"),
  ts: 1597520048816000,
  history_days: 30,
  name: 'posts'
}
```

## Indexes

Now we'll create an index for retrieving our posts.

```javascript
CreateIndex({
  name: "posts_by_title",
  source: Collection("posts"),
  terms: [{ field: ["data", "title"] }]
})
```

```javascript
{
  ref: Index("posts_by_title"),
  ts: 1597520075780000,
  active: true,
  serialized: true,
  name: 'posts_by_title',
  source: Collection("posts"),
  terms: [ { field: [ 'data', 'title' ] } ],
  partitions: 1
}
```

## Create

The `Create` function adds a new document to a collection. Let's create our first blog post:

```javascript
Create(
  Collection("posts"),
  { data: { title: "Deno is a secure runtime for JavaScript and TypeScript" } }
)
```

```javascript
{
  ref: Ref(Collection("posts"), "273952266465051144"),
  ts: 1597520090502000,
  data: { title: 'Deno is a secure runtime for JavaScript and TypeScript' }
}
```

## Map

We can create multiple blog posts with the `Map` function. We are calling `Map` with an array of posts and a `Lambda` that takes `"post_title"` as it's only parameter. `"post_title"` is then used inside the Lambda to provide the `title` field for each new post.

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

```javascript
[
  {
    ref: Ref(Collection("posts"), "273952274233950733"),
    ts: 1597520097930000,
    data: {
      title: 'YugabyteDB is an open source, high-performance, distributed SQL database for global, internet-scale apps'
    }
  },
  {
    ref: Ref(Collection("posts"), "273952274233951757"),
    ts: 1597520097930000,
    data: {
      title: 'NextJS is a React framework for building production grade applications that scale'
    }
  }
]
```

## Get

The `Get` function retrieves a single document identified by `ref`. We can query for a specific post by using its ID.

```javascript
Get(Ref(Collection("posts"), "207089200754852360"))
```

```javascript
{
  ref: Ref(Collection("posts"), "273952274233951757"),
  ts: 1597520097930000,
  data: {
    title: 'NextJS is a React framework for building production grade applications that scale'
  }
}
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

```javascript
{
  ref: Ref(Collection("posts"), "273952266465051144"),
  ts: 1597520090502000,
  data: { title: 'Deno is a secure runtime for JavaScript and TypeScript' }
}
```

So at this point we have our Redwood app set up with just a single:
* **Page** - `HomePage.js`
* **Cell** - `PostsCell.js`
* **Function** - `graphql.js`
* **SDL** - `posts.sdl.js`
* **Lib** - `db.js`
* **Service** - `posts.js`



We used FQL functions in the Fauna Shell to create a database and seed it with data. FQL functions included:
* **CreateCollection** - Create a collection
* **CreateIndex** - Create an index
* **Create** -
Create a document in a collection
* **Map** - Applies a function to all array items
* **Lambda** - Executes an anonymous function
* **Get** - Retrieves the document for the specified reference
* **Match** - Returns the set of items that match search terms

If we look at our home page we're currently getting an error from our PostsCell.

![04-PostsCell-Error](https://dev-to-uploads.s3.amazonaws.com/i/oq03w7q6ivch6zx1yyv9.jpg)

We're not getting the `message` data being pased into the Failure function, so let's run a query with GraphiQL on `http://localhost:8911/graphql`.

![05-posts-query](https://dev-to-uploads.s3.amazonaws.com/i/r5avhbe9x1mbgzy0s7kn.jpg)

When we run the query we get the following error.

![06-error-message](https://dev-to-uploads.s3.amazonaws.com/i/cu98d6xc6yn6g9yoghgp.jpg)

Based on the stacktrace it looks like we did not properly initialize our `db` variable with `faunadb.Client`. This is part of FaunaDB's [JavaScript driver](https://docs.fauna.com/fauna/current/drivers/javascript)

![07-stacktrace](https://dev-to-uploads.s3.amazonaws.com/i/u1ttwbydvgn9vw4z2nq2.jpg)

We also get the following message in our terminal running the dev server.

![08-terminal-error](https://dev-to-uploads.s3.amazonaws.com/i/88qysy3uwr318qgn59lb.jpg)