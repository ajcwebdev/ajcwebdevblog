---
title: redwood
date: "2020-05-31"
description: opinionated, full-stack, serverless web application framework for the jamstack
---

Introduction
* Redwood Philosophies
* Full Stack React
* Jamstack
* Serverless

Tutorial
* Part 1 - Setup
* Part 2 - Routes
* Part 3 - Prisma
* Part 4 - CRUD
* Part 5 - Contact
* Part 6 - GraphQL
* Part 7 - Deploy
* Part 8 - Auth

Reflection
* Podcasts
* Blogging

>*Full stack web application development is the next evolution of JAMstack. That becomes a primary place that you would deploy a full stack web application, and that’s what RedwoodJS is about.*
>
>***Tom Preston-Werner***
>***[Redwood brings full-stack to the JAMstack (March 12, 2020)](https://changelog.com/jsparty/119)***

![redwood-logo](https://dev-to-uploads.s3.amazonaws.com/i/zm6hfjusl47tlaooxqdu.png)

Redwood is an opinionated, full-stack, serverless web application framework for building and deploying JAMstack applications. Imagine:

* React frontend

* Statically delivered by CDN

* Talking via GraphQL to backend

* Backend running on AWS Lambdas

* All deployable with `git` push

![Alt Text](https://dev-to-uploads.s3.amazonaws.com/i/6q1mh8r0weq11kbfogta.png)

## Redwood Philosophies

#### There is power in standards about which tech to use, how to organize code into files, and how to name things

#### Relational databases like PostgreSQL and MySQL are still the workhorses of today's web apps

#### Operate in a serverless mindset and deploy to a generic computational grid

#### To deploy your application, you should only need to commit and push to your Git repository

#### To scale from zero to thousands of users should not require your intervention

#### Useful for writing simple, toy applications and complex, mission-critical applications

#### JavaScript can be the primary language on both frontend and backend

## Universal Deployment Machine

>*My dream of a future is for something I call a universal deployment machine, which means I write my code. It's all text. I just write text. Then I commit to GitHub. Then it's picked up and it's deployed into reality. That's it. That's the whole thing. That's what I want. That's what I've been looking for.*
>
>***Tom Preston Warner***
>***[RedwoodJS Shoptalk (May 11, 2020)](https://shoptalkshow.com/412/)***

# Full Stack React

There has recently been a sudden influx of different projects aiming to build a ***Full Stack React*** framework. What are people talking about when they say full stack react and why is it suddenly such a hot topic? A long running emphasis throughout the history of React has been its identification as a library instead of a framework. The one-liner for React has always been ***a JavaScript library for building user interfaces***.

It unapologetically focused on the view layer and did not seek to provide strong conventions around routing, server rendering, static site generation, or database integration. Instead projects like React Router, Relay, and Redux were created to solve some of these problems while remaining their own separate codebases. In contrast Nextjs and Gatsby built conventions on top of React.

As React has continued to maintain its popularity in JavaScript development there has been an increasing sentiment among some developers that the need for a true full stack React solution was greater than ever.

Developers that cut their teeth on projects like Rails, Ember, and Laravel are especially adamant that the tendency for React developers to create their own bespoke architectures is counterproductive and costly. Adam Wathan and Michael Chan have been long time advocates of this perspective.

I became interested in this topic in March when I listened to their conversation ***[React Is Not a Rails Competitor](https://www.fullstackradio.com/episodes/136)*** on Full Stack Radio. This podcast was released in the wake of three different frameworks that emerged in quick secession to tackle this problem: [***RedwoodJS***]((https://github.com/redwoodjs/redwood/commit/e2ceb0dcdffe4c28ff3ce804445387f4749e6a0b)), [***Blitz.js***](https://twitter.com/flybayer/status/1229425878481793024), and [***Remix***](https://twitter.com/remix_run/status/1253043162714525696).

# Jamstack

>*Jekyll is a simple, blog aware, static site generator.*
>
>***Tom Preston-Werner***
>***[Blogging Like a Hacker (November 17, 2008)](https://tom.preston-werner.com/2008/11/17/blogging-like-a-hacker.html)***

In 2008, Tom Preston-Werner published a blog post titled “Blogging Like a Hacker,” which told his story of blogging, programming, and his eventual invention of Jekyll. Jekyll was a reaction against complicated blog engines like WordPress.

His constraints included the ability to style his own blog and host it on the domain of his choosing. This eliminated wordpress.com and blogger.com. He mentioned that some people use GitHub as a blog but he considered that an impedance mismatch.

![Image](https://sedaily-topics.s3.amazonaws.com/topic_images/0_6513975690444203.png)

He decided to approach blogging from a software developers perspective. His writing would be stored in a Git repository and published via a deploy script or post-commit hook. A static site would be preferable to a dynamic site to keep complexity at a minimum. The blog would need to be easily customizable.

Jekyll works by:
1. Taking a template directory representing the raw form of a website
2. Running it through Textile and Liquid converters
3. Spiting out a complete, static website
4. Serving with Apache or similar web server

![Image](https://sedaily-topics.s3.amazonaws.com/topic_images/0_6838986812671863.png)

>*I was tired of having my blog posts end up in a database off on some remote server. That is backwards. I’ve lost valuable posts that way. I want to author my posts locally in Textile or Markdown. My blog should be easily stylable and customizable any way I please. It should take care of creating a feed for me. And most of all, my site should be stored on GitHub so that I never lose data again.*
>
>***Tom Preston-Werner***
>***[tpw](https://github.com/mojombo/tpw)***

Numerous projects influenced by Jekyll appeared in the following years.

* Thomas Reynolds created [Middleman](https://awardwinningfjords.com/2009/10/22/middleman.html), a static site generator utilizing Haml and Sass in [2009](https://github.com/middleman/middleman/commit/493089d4b0ebdb64524695dc4fe4e703ddeec536)
* Alexis Metaireau created [Pelican](https://blog.john-pfeiffer.com/how-to-set-up-a-pelican-static-blog-site/), a Python project that converts static text files into html sites in [2010](https://github.com/getpelican/pelican/commit/00cf9644d8a85e98cf6eb6c0ebf32cf03046f0ee)
* Tommy Chen created [Hexo](https://hexo.io/), a blog framework powered by Node.js in [2012](https://github.com/hexojs/hexo/commit/6129b2fd773ffafa0bf5626df26b72e7e8f7ad7c)
* Jeff Escalante created [Roots](https://roots.netlify.app/), a static site compiler written in CoffeeScript, in [2012](https://github.com/jescalan/roots/commit/5b3b93585e9accb43f67178ba6e1bc1e66f21ff6)
* Steve Francia created [Hugo](https://spf13.com/post/go-go-hugo-blog/), a static site generator written in Go [in 2013](https://github.com/gohugoio/hugo/commit/50a1d6f3f155ab837310e00ffb309a9199773c73)

![Image](https://sedaily-topics.s3.amazonaws.com/topic_images/0_1401401717454267.png)

## Staticgen

>*There are those who describe Netlify as “GitHub Pages on Steroids”. If that’s the case then Hugo on Netlify must be digging into Lance Armstrong’s stash.*
>
>***Mathias Biilmann***
>***[Hosting Hugo on Netlify–Insanely Fast Deploys (July 30, 2015)](https://www.netlify.com/blog/2015/07/30/hosting-hugo-on-netlifyinsanely-fast-deploys/)***

In 2014, Mathias Biilmann Christensen created [staticgen.com](http://mathias-biilmann.net/posts/2014/07/01/staticgen), a leaderboard of top open-source static site generators. It uses a variety of metrics including GitHub stars, forks, and twitter followers to rank different static site generators.

Around that time Mathias was running MakerLoop, a content management startup based in San Francisco. He believed that Git-centered workflows with static site generators like Jekyll represented a massive change in the web development space. This lead to Mathias co-founding Netlify with his childhood friend Christian Bach. Tom Preston-Werner was an early investor in Netlify.

## Gatsby

Gatsby was created by Kyle Mathews in [2015](https://github.com/gatsbyjs/gatsby/commit/24606f5a2d5c85d7b6661403333f34823409bdf3). It started as a static site generator built with React, but as the project grew it no longer functioned as simply a static site generator, and Kyle found the term to be ill fitting to the project.

Gatsby incorporated GraphQL and increasingly used sophisticated 3rd party APIs to perform various dynamic tasks that could not be achieved with older static site generators. Other projects appeared that were influenced by Gatsby including [Gridsome](https://gridsome.org/) and [Scully](https://www.netlify.com/blog/2019/12/16/introducing-scully-the-angular-static-site-generator/).

This new paradigm started to be referred to as the [JAMstack](https://jamstack.org/), as in JavaScript, APIs, and Markup. Mathias credits [Andreas Sæbjørnsen](https://changelog.com/podcast/251) with first coining the term. Recently there has been a push to refer to it simply as Jamstack in an attempt to distance itself from the original acronym ([see JAMstack vs. Jamstack by Chris Coyier](https://css-tricks.com/jamstack-vs-jamstack/)). The Jam has been slowly spreading ever since.

![Image](https://sedaily-topics.s3.amazonaws.com/topic_images/0_7525431285920556.jpg)

# Serverless

# Tutorial

# Part 1 - Setup

# Part 2 - Routes

# Part 3 - Prisma

# Part 4 - CRUD

# Part 5 - Contact

# Part 6 - GraphQL

# Part 7 - Deploy

# Part 8 - Auth

# Reflection

# Podcasts
# Blogging