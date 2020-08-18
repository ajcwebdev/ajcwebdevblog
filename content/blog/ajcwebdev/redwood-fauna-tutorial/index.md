# Building a Minimum Viable Stack with RedwoodJS and FaunaDB

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
  * Match

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

Create a folder in `web/src/components` called `PostsCell` and inside that folder create a file called `PostsCell.js` with the following code:

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

import faunadb from "faunadb"

export const db = new faunadb.Client({ secret: process.env.FAUNADB_SECRET });
```

## Services

In our services folder we'll create a `posts` folder with a file called `posts.js`. Services are where Redwood centralizes all business logic. These can be used by your GraphQL API or any other place in your backend code.

```javascript
// api/src/services/posts/posts.js

import { query as q } from "faunadb"
import { db } from 'src/lib/db'

export const posts = () => {
  return db.query(q.Map(
    q.Paginate(q.Match(q.Index("all_posts"))),
    q.Lambda("postRef", q.Get(q.Var("postRef")))))
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

First we will install the `fauna-shell` which will let us easily work with our database from the terminal.

```
npm install -g fauna-shell
```

Then we will install the `faunadb` client. `cd` into the `api` folder and run the following command:

```
yarn add faunadb
```

Now we'll login to our Fauna account so we can access a database with the shell.

```
fauna cloud-login
```

You'll be asked to verify your email and password. If you signed up for FaunaDB using your GitHub or Netlify credentials, follow [these steps](https://docs.fauna.com/fauna/current/start/cloud-github), then skip the Create new Database section and continue this tutorial at the beginning of the Collections section.

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
  ts: 1597718505570000,
  history_days: 30,
  name: "posts"
}
```

## Create

The `Create` function adds a new document to a collection. Let's create our first blog post:

```javascript
Create(
  Collection("posts"),
  {
    data: {
      title: "Deno is a secure runtime for JavaScript and TypeScript"
    }
  }
)
```

```javascript
{
  ref: Ref(Collection("posts"), "274160525025214989"),
  ts: 1597718701303000,
  data: {
    title: "Deno is a secure runtime for JavaScript and TypeScript"
  }
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
      Collection("posts"),
      {
        data: {
          title: Var("post_title")
        }
      }
    )
  )
)
```

```javascript
[
  {
    ref: Ref(Collection("posts"), "274160642247624200"),
    ts: 1597718813080000,
    data: {
      title:
        "YugabyteDB is an open source, high-performance, distributed SQL database for global, internet-scale apps"
    }
  },
  {
    ref: Ref(Collection("posts"), "274160642247623176"),
    ts: 1597718813080000,
    data: {
      title:
        "NextJS is a React framework for building production grade applications that scale"
    }
  }
]
```

## Get

The `Get` function retrieves a single document identified by `ref`. We can query for a specific post by using its ID.

```javascript
Get(
  Ref(
    Collection("posts"), "274160642247623176"
  )
)
```

```javascript
{
  ref: Ref(Collection("posts"), "274160642247623176"),
  ts: 1597718813080000,
  data: {
    title:
      "NextJS is a React framework for building production grade applications that scale"
  }
}
```

## Indexes

Now we'll create an index for retrieving all the posts in our collection.

```javascript
CreateIndex({
  name: "all_posts",
  source: Collection("posts")
})
```

```javascript
{
  ref: Index("all_posts"),
  ts: 1597719006320000,
  active: true,
  serialized: true,
  name: "all_posts",
  source: Collection("posts"),
  partitions: 8
}
```

## Match

`Index` returns a reference to an index which `Match` accepts and constructs a set. `Paginate` takes the output from Match and returns a Page of results fetched from Fauna. Here we are returning an array of references.

```javascript
Paginate(
  Match(
    Index("all_posts")
  )
)
```

```javascript
{
  data: [
    Ref(Collection("posts"), "274160525025214989"),
    Ref(Collection("posts"), "274160642247623176"),
    Ref(Collection("posts"), "274160642247624200")
  ]
}
```

## Lambda

We can get an array of references to our posts, but what if we wanted an array of the actual data contained in the reference? We can `Map` over the array just like we would in any other programming language.

```javascript
Map(
  Paginate(
    Match(
      Index("all_posts")
    )
  ),
  Lambda(
    'postRef', Get(Var('postRef'))
  )
)
```

```javascript
{
  data: [
    {
      ref: Ref(Collection("posts"), "274160525025214989"),
      ts: 1597718701303000,
      data: {
        title: "Deno is a secure runtime for JavaScript and TypeScript"
      }
    },
    {
      ref: Ref(Collection("posts"), "274160642247623176"),
      ts: 1597718813080000,
      data: {
        title:
          "NextJS is a React framework for building production grade applications that scale"
      }
    },
    {
      ref: Ref(Collection("posts"), "274160642247624200"),
      ts: 1597718813080000,
      data: {
        title:
          "YugabyteDB is an open source, high-performance, distributed SQL database for global, internet-scale apps"
      }
    }
  ]
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
* **Create** - Create a document in a collection
* **Map** - Applies a function to all array items
* **Lambda** - Executes an anonymous function
* **Get** - Retrieves the document for the specified reference
* **CreateIndex** - Create an index
* **Match** - Returns the set of items that match search terms
* **Paginate** - Takes a Set or Ref, and returns a page of results