---
title: a first look at redwood.js
date: "2020-08-10"
description: complete series
---

# Introduction

## [I - Redwood Philosophies](https://dev.to/ajcwebdev/redwood-1d46)

***RedwoodJS*** is an opinionated, full-stack, serverless web application framework for the Jamstack. It is designed to enable the dream of a Universal Deployment Machine.

## [II - Full Stack React](https://dev.to/ajcwebdev/full-stack-react-1ihi)

There has recently been an influx of different projects aiming to build a ***Full Stack React*** framework. What are people talking about when they say Full Stack React and why is it suddenly such a hot topic?

## [III - Jamstack](https://dev.to/ajcwebdev/a-short-history-of-the-jamstack-3lk7)

The ***Jamstack*** is a departure from traditional server-rendered stacks like LAMP and MEAN. Jamstack applications serve static files from globally distributed CDN's, removing the server and the database from the stack entirely and replacing them with APIs that provide dynamic functionality.

## [IV - Serverless](https://ajcwebdev.substack.com/p/42-a-short-history-of-serverless)

***Serverless*** is a buzz word commonly used to refer to Function-as-a-Service cloud products like AWS Lambda. Instead of paying for a server to always be running and ready to accept requests, you pay based on the specific number of function calls your app invokes.

# Tutorial

## [Part 1 - Setup](https://dev.to/ajcwebdev/a-first-look-at-redwood-js-1017)

**Install and create our first Redwood application.**

This series will start at the very beginning and assume no prior knowledge of Redwood. We'll install the Redwood CLI and learn how to use Redwood's custom generators to create pages.

## [Part 2 - Routes](https://dev.to/ajcwebdev/a-first-look-at-redwood-js-part-2-44ph)

**Explore Redwood's router and create links for our pages.**

Redwood has its own built-in router inspired by Ruby on Rails, React Router, and Reach Router. Redwood Router is designed to list all routes in a single file, without any nesting.

## [Part 3 - Prisma](https://dev.to/ajcwebdev/a-first-look-at-redwood-js-part-3-5ao5)

**Get our database up and running and learn to create, retrieve, update, and destroy blog posts.**

Prisma 2.0 is a query builder that provides a type-safe API for submitting database queries that return JavaScript objects. We'll learn how to write a Prisma schema file and use it to initialize our database.

## [Part 4 - CRUD](https://dev.to/ajcwebdev/a-first-look-at-redwood-js-part-4-2m0g)

**Explain all the generated code for performing CRUD operations and set up our frontend to render a list of our blog posts by querying data from our backend.**

This part goes deep into the code that Redwood writes for you. How is Redwood handling form data? What is the CLI spitting out when we generate pages or cells? What is a GraphQL schema definition language? What does all this have to do with services? Finally we'll generate a cell that queries our backend and renders all our blog posts to the front page of our site. 

## [Part 5 - Contact](https://dev.to/ajcwebdev/a-first-look-at-redwood-js-part-5-2ol4)

**Combine everything we've learned up to this point to generate a contact page and take input from a user.**

We'll go deep into Redwood forms and all the corresponding helpers that make our lives easier when working with forms. Redwood uses react-hook-form by default but it can also use other React form builders.

## [Part 6 - GraphQL](https://dev.to/ajcwebdev/a-first-look-at-redwood-js-part-6-a25)

**Connect our contact form to the database to persistent data entered into the form.**

After creating our contact form we need to create a new contact schema and migrate our database. We'll use another Redwood generator to create our schema definition language and our GraphQL resolvers for our services.

## [Part 7 - Deploy](https://dev.to/ajcwebdev/a-first-look-at-redwood-js-part-7-22b0)

**Deploy our frontend application with Serverless functions on Netlify and our backend to a hosted Postgres database on Heroku.**

A website isn't very useful unless it's on the web. In this part we'll deploy our React frontend to Netlify with their Serverless functions. Netlify will give us a free domain that we can share with the world. For our backend we'll use Heroku to host our database with Postgres.

## [Part 8 - Auth](https://dev.to/ajcwebdev/a-first-look-at-redwood-js-part-8-3pjc)

**Implement role-based authentication with Netlify Identity.**

In the final part of our series we'll use Netlify Identity to implement role-based authentication on our blog. We'll use one more Redwood generator for authentication. We'll be able to use Netlify's login functionality so we don't have to make our own login form. Redwood Router gives us built in private routes for controling exactly which parts of our app are accessible to the public and which are locked down.

# Reflection

## Podcasts, Blogging, and Open Source