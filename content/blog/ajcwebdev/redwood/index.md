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

**There is power in standards about which tech to use, how to organize code into files, and how to name things**

**Relational databases like PostgreSQL and MySQL are still the workhorses of today's web apps**

**Operate in a serverless mindset and deploy to a generic computational grid**

**To deploy your application, you should only need to commit and push to your Git repository**

**To scale from zero to thousands of users should not require your intervention**

**Useful for writing simple, toy applications and complex, mission-critical applications**

**JavaScript can be the primary language on both frontend and backend**

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

> *It's 2012, I get hired into AWS and it's my first day there. And my boss Alyssa Henry, who at that time is running all of storage, so S3, EBS, like the whole storage division for AWS sits me down at lunch and says,*
>
> *"Okay, Tim, so here's the deal. We heard from customers that they love S3. It's simple, it's easy to use. It's a different kind of way of thinking about the cloud. They love all of that, but it's just a storage solution, right? There's no way to ... Let's say you store an image, there is no way to make a thumbnail of it. You pull out a compressed file, there's no easy way to decompress it on the fly plus the other million things developers might want to do with the stuff that they're storing in here. So they've told us this in customer advisory meetings and one on ones, see if he can do something with that. Okay. I'm busy, got to run. Good luck."*
>
> *So this is day one for me at AWS. This is literally my very first conversation coming out of the sort of the onboarding and signing up all the paperwork. So I'm like,*
>
> *"Okay, grow a business in the cloud. Make it easy and think about S3 as a kind of inspiration."*
>
> *We had to make the cloud as easy for someone who does applications and business logic as it is for someone with a PhD in distributed systems. And that's when we realized like there was some there, there. And so we got excited about that. We came up with this idea for event hookup and we were kind of off to the races.*
>
> ***Tim Wagner***
>***[The Past, Present, and Future of Serverless (June 8, 2020)](https://www.serverlesschats.com/52/)***

![](https://cdn.substack.com/image/fetch/w_1456,c_limit,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fbucketeer-e05bbc84-baa3-437e-9518-adb32be77984.s3.amazonaws.com%2Fpublic%2Fimages%2F090fdbbd-e1a0-45bc-8ef9-d8833254e983_1600x800.png)

Serverless is a made up buzz word that is also commonly used to refer to Function-as-a-Service cloud products like [AWS Lambda](https://aws.amazon.com/lambda/), [Azure Functions](https://azure.microsoft.com/en-us/services/functions/), and [Google Cloud Functions](https://cloud.google.com/functions). The basic premise is that instead of paying for a server to always be running and ready to accept requests, you pay based on the specific number of function calls your app invokes.

It was pioneered by Tim Wagner’s team at Amazon Web Services in 2012 and has become a popular paradigm for “cloud native” applications, which are applications designed specifically to run on a platform like AWS, Azure, GCP, Digital Ocean, or Linode. Tim Wagner served as general manager for Lambda, [API Gateway](https://aws.amazon.com/api-gateway/), and the [Serverless Application Repository](https://aws.amazon.com/serverless/serverlessrepo/).

> *The computers would handle a number of problems concurrently. Organizations would have input-output equipment installed on their own premises and would buy time on the computer much the same way that the average household buys power and water from utility companies.*
>
> ***W. F. Bauer***
>***[Computer design from the programmer's viewpoint (1958)](https://dl.acm.org/doi/10.1145/1458043.1458055)***

It has much in common philosophically with the Jamstack but is a more general paradigm building on work going back to [Multics](https://en.wikipedia.org/wiki/Multics) and other [time-sharing systems](https://en.wikipedia.org/wiki/Time-sharing) of the 1960s.

![aws-lambda](https://cdn.substack.com/image/fetch/w_1456,c_limit,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fbucketeer-e05bbc84-baa3-437e-9518-adb32be77984.s3.amazonaws.com%2Fpublic%2Fimages%2F0e80f909-47e4-4fa0-b7bd-df9817602242_951x276.png)

In 2015 the Serverless Framework open source project was released, and eventually lead to the creation of a company called Serverless, Inc. This successfully confused everyone about the meaning of the term serverless to an even greater degree than before. In reference to the term, Serverless founder Austen Collins claimed it was, "[***not technically accurate***](https://techcrunch.com/2016/10/12/serverless-raises-3m-to-help-developers-go-serverless/)."

# Part 1 - Setup

>*I like to think that most things can be achieved. Whatever you have in your head you can probably pull off with code as long as it's possible within the constraints of the universe. It's just a matter of time... and money... and attention.*  
>
>***Tom Preston-Werner***
>***[Full Stack Radio 138](https://www.fullstackradio.com/episodes/138)***

[Redwood](https://dev.to/ajcwebdev/redwood-1d46) is an opinionated, full-stack, serverless web application framework for building and deploying Jamstack applications.

I've structured the article to reflect the actual process I go through when experimenting with a new framework for the first time. I stick to the path laid out in the official docs tutorial, but as I go through each step I reference the documentation for each command or component. This helps me build a mental model of the framework instead of just copy-pasting commands and code snippets.

I will start at the very beginning and assume no prior knowledge of Redwood although I do assume a basic knowledge of React. But I'm talking really basic, if you know what a component is, have written at least a dozen lines of JSX, and have generated at least one project with [create-react-app](https://reactjs.org/docs/create-a-new-react-app.html) then you'll be fine.

If none of that made sense you should click the link to the create-react-app docs and work through those before reading this. This article is geared towards someone who has at least a few months experience in a coding bootcamp or on the job, around the point where they start getting comfortable with the basic workflows of git, npm, the terminal, and simple HTML websites.

You'll need `yarn` for this tutorial which has slight differences from `npm`. If you've never used `yarn` you can find installation instructions [here](https://yarnpkg.com/getting-started/install) or just enter `yarn install` into your terminal.

# `yarn create redwood-app`

The first step is to install Redwood globally to my system and generate our first project. We'll accomplish both of these with the `yarn create` command.

![01-yarn-create-redwood-app](https://dev-to-uploads.s3.amazonaws.com/i/6fe6msthvip5b2ff8r1t.jpg)

This will create a folder called `ajcwebdev` that holds all the code that will be generated. You can call your project anything you want, just make sure to keep using your name anytime I use `ajcwebdev` in a terminal command.

![02-yarn-creating-redwood-app](https://dev-to-uploads.s3.amazonaws.com/i/cjaeklfvncspim7wlodu.jpg)

# `yarn redwood dev`

`yarn rw` is the same as `yarn redwood` and can be used to save a few keystrokes if you want. We'll `cd` into that folder and then start our development server.

![03-cd-yarn-redwood-dev](https://dev-to-uploads.s3.amazonaws.com/i/i30ds3opi4rgswptijbh.jpg)

`yarn redwood dev` can be used to run a development server for the Redwood server, Webpack server or your database "server" which isn't exactly a server.

![04-yarn-redwood-dev](https://dev-to-uploads.s3.amazonaws.com/i/y4mlr95xq35kbtn6vlu9.jpg)

Don't worry about any of that for now but that'll be important in later articles.

You may also get an error that says `Error: @prisma/client did not initialize yet. Please run "prisma generate" and try to import it again.`

![05-prisma-error](https://dev-to-uploads.s3.amazonaws.com/i/mqsa1lez5v5vxqawfwv8.jpg)

For the rest of the stuff I do in this article I did not have any trouble so I'm going to be ignoring that for now.

Our server is now running on localhost:8910 (a mnemonic to help remember that is thinking of counting 8-9-10). Open a web browser and enter localhost:8910 into the address bar. If you've done everything correctly up to this point you'll see the Redwood starter page.

![06-redwood-starter-page](https://dev-to-uploads.s3.amazonaws.com/i/ycisyl2bbxasa9j6zr9b.jpg)

WHOOPS, it worked, we're up and running.

Don't worry too much about what it says about custom routes, we'll talk about that in the next article. Lets look at the file structure that has been created for us.

![07-project-structure](https://dev-to-uploads.s3.amazonaws.com/i/fjo3yan8dvi0geynn6or.jpg)

Don't worry about most of this, for the purpose of this article we'll only be working in the `web` folder. Since we are responsible developers the first thing we do is go to the README.

![08-README](https://dev-to-uploads.s3.amazonaws.com/i/7ox6y0oe85s9o9j8bj8d.jpg)

The README provides instructions for the commands that we used earlier to get our application set up, `yarn install` and `yarn redwood dev`. It also mentions something you may have noticed earlier, we have something else running on `localhost:8911`.

![09-serverless-functions](https://dev-to-uploads.s3.amazonaws.com/i/vjbt2amtwrz4nmv6qqxm.jpg)

Once again, don't worry if that doesn't make sense since it's outside the scope of this part.

In Redwood our frontend code is contained in the `web` folder and our backend code is contained in the `api` folder. Lets look at our `web` folder.

![10-project-structure-web](https://dev-to-uploads.s3.amazonaws.com/i/3ouxm52ot3p6r1sc9y54.jpg)

Redwood structures the `web` folder a bit like create-react-app projects with a `public` and `src` folder but the index.html file that renders our root component is in the `src` folder instead of `public`.

# `redwood generate page`

With our application now set up we can start creating pages. We'll use the `generate page` command to create a home page and a folder to hold that page.

![11-yarn-redwood-generate-page-home](https://dev-to-uploads.s3.amazonaws.com/i/1w9jbx6nva7vec9pvllf.jpg)

This created files for our home page and another file for testing that page.

![12-yarn-redwood-generating-HomePage](https://dev-to-uploads.s3.amazonaws.com/i/okmjl4hxk5ux0tb7g1p7.jpg)

Since I only entered `home` it will use that to name both the folder and the component file but you can specify each if necessary.

![13-project-structure-web-src-pages](https://dev-to-uploads.s3.amazonaws.com/i/vaoq73eoxk6nz5qo6aev.jpg)

Return to your browser and you will now see a new page instead of the landing page.

![14-HomePage](https://dev-to-uploads.s3.amazonaws.com/i/mogitc893pv03j68lz9q.jpg)

Let's look at the code that was generated for this page. It's a component called `HomePage` that returns a `<div>` with a header `<h1>` and a paragraph tag `<p>`.

![15-HomePage-component](https://dev-to-uploads.s3.amazonaws.com/i/ejcu3z1rm630xxmxotqx.jpg)

This should be pretty self-explanatory if you have experience with React. If this doesn't look familiar to you then you should take a little time to study React by itself before jumping into Redwood. Now we'll edit the page and see what happens.

![16-HomePage-edit](https://dev-to-uploads.s3.amazonaws.com/i/8f0c42emzcmskgymii1w.jpg)

Feel free to include links to your own social accounts. With those changes made return to your browser.

![17-HomePage-new](https://dev-to-uploads.s3.amazonaws.com/i/hn5a8lp4b1oqfy3xhavo.jpg)

Now we are going to generate our `about` page.

![18-yarn-redwood-generate-page-about](https://dev-to-uploads.s3.amazonaws.com/i/h3lunfia2zs8dn0l9mq1.jpg)

Like before we created an `AboutPage` component inside of an `AboutPage` folder along with a file for testing that page.

![19-yarn-redwood-generating-AboutPage](https://dev-to-uploads.s3.amazonaws.com/i/k5k2ae5jzazrac5ksm27.jpg)

We don't yet have a link to get to it from the home page, so for now you'll need to enter the route manually into your browser address bar by adding `/about` after `localhost:8910`.

![20-AboutPage](https://dev-to-uploads.s3.amazonaws.com/i/bsv9l45ikjfbxcgyewb3.jpg)

Open up the code and it's another React component much like the last! Components are kind of a big deal in React.

![21-AboutPage-component](https://dev-to-uploads.s3.amazonaws.com/i/fapy9aa8ticdut1cftsf.jpg)

We can also edit this page just like the `home` page.

![22-AboutPage-edit](https://dev-to-uploads.s3.amazonaws.com/i/tbeillfms6a7m9gi0n3c.jpg)

With those changes return to your browser.

![23-AboutPage-new](https://dev-to-uploads.s3.amazonaws.com/i/iz3zabuptlphfcctcsd6.jpg)

We can also see these files have been added to our `src` folder.

![24-project-structure-web-new](https://dev-to-uploads.s3.amazonaws.com/i/w8nz5fcatytkyju9ty1d.jpg)

In the [next part](https://dev.to/ajcwebdev/a-first-look-at-redwood-js-part-2-44ph) we'll take a look at Redwood's router and create links for the pages we created.

# Part 2 - Routes

> *We basically wrote the tutorial the way that we wanted the code to work and then we made the tutorial work by writing the code. As opposed to [Readme Driven Development](https://tom.preston-werner.com/2010/08/23/readme-driven-development.html) which I've written about this is tutorial driven development.*  
>
>***Tom Preston-Werner***
>***[Full Stack Radio 138](https://www.fullstackradio.com/episodes/138)***

In [part 1](https://dev.to/ajcwebdev/a-first-look-at-redwood-js-1017) we installed and created our first RedwoodJS application. We used `yarn create redwood-app` to generate the initial app and `redwood generate page` to create a `HomePage` folder containing a `HomePage` file containing a `HomePage` component along with an `AboutPage` folder containing an `AboutPage` file containing an `AboutPage` component.

We were able to navigate between the different pages in our browser by entering `/about` for the about page or a slash (`/`) for the home page. Depending on your experience with React this may have been surprising to you.

If you've worked on routing in React before you know that to achieve this there needs to be an entirely different package imported containing the router and then your routes need to be wrapped in a `<BrowserRouter>` or `<Router>` component to give the router access to your pages. Well guess what.....

# `Routes.js`

![01-web-src-routes](https://dev-to-uploads.s3.amazonaws.com/i/qjzms9pgwvboxzisnpdq.jpg)

In our `src` folder we have a file called `Routes.js`. When we used the CLI to generate `HomePage` and `AboutPage` we also created these routes.

* All Page components from 'src/pages` are auto-imported
* Nested directories are supported, and should be uppercase
* Each subdirectory will be prepended onto the component name

Examples:

`src/pages/HomePage/HomePage.js`         -> `HomePage`
`src/pages/Admin/BooksPage/BooksPage.js` -> `AdminBooksPage`

# `index.js`

The other file in our `src` folder is `index.js` which is our root component that ReactDOM renders to the screen.

![02-web-src-index](https://dev-to-uploads.s3.amazonaws.com/i/xzttnicig89d6xskt5c6.jpg)

In React all [components are composable](https://reactjs.org/blog/2013/06/05/why-react.html) which encourages the creation of reusable UI components that present data that changes over time. Traditionally, web application UIs were built using templates or HTML directives.

But in React you always have a root component that contains other components and those components may contain other components. If that's a little confusing just give it some time and it'll start to click as this series goes on.

The important take away is:

1. Your routes and thus all the website's pages are contained within the `<RedwoodProvider>` tags (we'll talk about these more once we get to state management).
2. The provider itself is contained within the `<FatalErrorBoundary>` component that is taking in `<FatalErrorPage>` as a prop which defaults your website to an error page if all else fails.

# `Link`

When it comes to routing, matching URLs to Pages is only half the equation. The other half is generating links to your pages. Lets add a link to our page so we can navigate between our home page and about page by clicking on the page. We'll need to add 3 things to our `HomePage` file:

1. Import `Link` and `routes` from `@redwoodjs/router`
2. `<Link to={}>About</Link>`
3. Pass into the Link component `routes.about()`

![03-HomePage-link-to-about-page](https://dev-to-uploads.s3.amazonaws.com/i/f9xkqr5045j6iu9si4m1.jpg)

### named route functions

You use a `Link` to generate a link to one of your routes and can access URL generators for any of your routes from the `routes` object. We call the functions on the `routes` object ***named route functions*** and they are named after whatever you specify in the `name` prop of the `Route`. This is a key term for the redwood mental model. Return to your browser to see the changes to your home page.

![04-home-page-with-about-link](https://dev-to-uploads.s3.amazonaws.com/i/3t6p5rlpwxqvey5admb0.jpg)

We now have a link we can click to navigate to our about page from our home page. Click the link and you will be brought to your about page.

![05-about-page](https://dev-to-uploads.s3.amazonaws.com/i/40086y4wtzrhxak5qbri.jpg)

We also want to be able to navigate back to our home page once we are on our about page. We'll do the same three steps from earlier but with a different prop:

1. Import `Link` and `routes` from `@redwoodjs/router`
2. `<Link to={}>About</Link>`
3. Pass into the Link component `routes.home()`

![06-AboutPage-component](https://dev-to-uploads.s3.amazonaws.com/i/0cox7ilggmdfs8kz10s5.jpg)

Everything is exactly the same except we pass in `routes.home()` instead of `routes.about()` because we want to navigate to our home page this time. Take a look at your about page.

![07-about-page-with-return-home-link](https://dev-to-uploads.s3.amazonaws.com/i/xz6g1u1vey407bbx1s0r.jpg)

There is now a link that will take you back to the home page when clicked. If we open up our editor and look at our working tree we can see the changes we added.

![08-AboutPage-working-tree](https://dev-to-uploads.s3.amazonaws.com/i/b3v2rq3qfmbmx5uj8659.jpg)

You can only see this if you're working with git and regularly committing and pushing your code which is highly recommended.

# Layout

You've probably been on a website before. Usually there's some kind of navigation bar at the top and footer at the bottom that stays consistent as you travel around the website. Redwood's folder structure is designed to make this really easy.

![09-layouts](https://dev-to-uploads.s3.amazonaws.com/i/8vc8q5i88vsytad8dsgr.jpg)

Remember what I said before about everything being a component containing other components? That's the middle part. Pages contain components. Your layout will contain all of your pages.

We can generate a file for our layout with `yarn redwood generate layout` or `yarn rw g layout`. Btw, if at any point you're having trouble remembering commands just enter:

![10-yarn-rw--help](https://dev-to-uploads.s3.amazonaws.com/i/yiy2tj9repgqp0187qz1.jpg)

and you'll get a quick reminder of all the commands.

![11-yarn-rw-commands](https://dev-to-uploads.s3.amazonaws.com/i/rjocasva57iluyltwprw.jpg)

# `generate layout`

This will work a lot like the `generate page` commands we've done earlier

![12-yarn-redwood-g-layout-blog](https://dev-to-uploads.s3.amazonaws.com/i/x3q31dwppbdt1szmrj02.jpg)

The only difference is it will create a folder inside `./web/src/layouts` this time instead of `./web/src/pages` because we are generating a layout and not a page.

![13-generating-BlogLayout](https://dev-to-uploads.s3.amazonaws.com/i/uzit8s41dxa5eafcjv8e.jpg)

That makes sense. Take a look at your layouts folder and you'll see a file called `BlogLayout.js` and another called `BlogLayout.test.js` for testing.

![14-BlogLayout-folder](https://dev-to-uploads.s3.amazonaws.com/i/03fwaru9jot6xg28zg1e.jpg)

# `BlogLayout` component

Lets look at our `BlogLayout` component

![15-layout-BlogLayout](https://dev-to-uploads.s3.amazonaws.com/i/wsne05s98qq85n2aoilu.jpg)

`children` is where the magic will happen. Any page content given to the layout will be rendered here.

![16-BlogLayout-component](https://dev-to-uploads.s3.amazonaws.com/i/3t1ackcgti53g9had7it.jpg)

Back to HomePage and AboutPage, we add a <BlogLayout> wrapper and now they're back to focusing on the content they care about

![17-Homepage-import-BlogLayout](https://dev-to-uploads.s3.amazonaws.com/i/o4nn6hsf23s3uq8gnfhv.jpg)

We can remove the import for Link and routes from HomePage since those are in the Layout instead:

![18-AboutPage-import-BlogLayout](https://dev-to-uploads.s3.amazonaws.com/i/3zsqpyzv5jb48xylpqgj.jpg)

Notice that the import statement uses `src/layouts/BlogLayout` and not `../src/layouts/BlogLayout` or `./src/layouts/BlogLayout`.
* This is a convenience feature so you don't need to worry about the nesting of your folders.
* `src` is an alias to the `src` path in the current workspace. If you're working in web then `src` points to `web/src` and in `api` it points to `api/src`.

If we look at our home pages now it should look and behave the same way as before except we have turned our title in the `<h1>` tag into a home page link.

![19-home-page-with-BlogLayout](https://dev-to-uploads.s3.amazonaws.com/i/469y1ctqit6xhbb5btu8.jpg)

Our about page is the same except we have removed the link to return home since we can now click the title.

![20-about-page-with-BlogLayout](https://dev-to-uploads.s3.amazonaws.com/i/fqrddthwkdjhgiyuos02.jpg)

In the [next part](https://dev.to/ajcwebdev/a-first-look-at-redwood-js-part-3-5ao5) we'll start working with a database and learn to create, retrieve, update, and destroy blog posts.

# Part 3 - Prisma

> *What I wanted was to codify and standardize the types of things that we were already doing and just remove choice and remove friction and just give people the ability to sit down and say, alright I know these technologies already, I have the prerequisite knowledge to do this.*  
>
>***Tom Preston-Werner***
>***[Full Stack Radio 138](https://www.fullstackradio.com/episodes/138)***

In [part 1](https://dev.to/ajcwebdev/a-first-look-at-redwood-js-1017) we installed and created our first RedwoodJS application and in [part 2](https://dev.to/ajcwebdev/a-first-look-at-redwood-js-part-2-44ph) we created links to our different page routes and a reusable layout for our site. In this part we'll get our database up and running and learn to create, retrieve, update, and destroy blog posts.

So far we've been working in the `web` folder. In our `api` folder there is a folder called `prisma` for our Prisma schema.

Prisma is a [query builder](https://www.prisma.io/docs/understand-prisma/why-prisma) that provides a type-safe API for submitting database queries which return JavaScript objects. It is similar to an ORM and was selected by Tom in the hopes of emulating [Active Record's](https://guides.rubyonrails.org/active_record_basics.html) role in Ruby on Rails.

![00-project-structure-api.jpg](https://dev-to-uploads.s3.amazonaws.com/i/4sisnx4k4e64iu1hfsic.jpg)

The Prisma schema file is the main configuration file for your Prisma setup. It is typically called `schema.prisma`

![01-schema-prisma.jpg](https://dev-to-uploads.s3.amazonaws.com/i/i572d9i7wt73ib2oio1l.jpg)

In order to set up Prisma Client, you need a Prisma schema file with:
* your database connection
* the Prisma Client `generator`
* at least one `model`

![02-schema-prisma-Post-model.jpg](https://dev-to-uploads.s3.amazonaws.com/i/q1yc2jpdjyslvlp54r39.jpg)

# `seeds.js`

`seeds.js` is used to populate your database with any data that needs to exist for your app to run at all (maybe an admin user or site configuration).

![03-seeds](https://dev-to-uploads.s3.amazonaws.com/i/46t9inuntle6618ov9v3.jpg)

# `db save`

Running `yarn rw db save` generates the folders and files necessary to create a new migration.

![04-yarn-redwood-db-save.jpg](https://dev-to-uploads.s3.amazonaws.com/i/uqln1ynyspzdmbu98ivy.jpg)

You will be asked to name your migration.

![05-creating-database-migration](https://dev-to-uploads.s3.amazonaws.com/i/68tg1nfsuqp3lefwexc0.jpg)

I entered `initialize-database` as the name of my migration.

![06-new-datamodel](https://dev-to-uploads.s3.amazonaws.com/i/aiogafas0oxb1xbgmy2z.jpg)

### Data sources

Specify the details of the data sources Prisma should connect to (e.g. a PostgreSQL database)

### Generators

Specifies what clients should be generated based on the data model (e.g. Prisma Client)

### Data model definition

Specifies your application models (the shape of the data per data source) and their relations

# `migrations`

A migration defines the steps necessary to update your current schema.

![07-created-your-migration](https://dev-to-uploads.s3.amazonaws.com/i/ubpbkdw7mctqvvass6eu.jpg)

The `migrate` command creates and manages database migrations. It can be used to create, apply, and rollback database schema updates in a controlled manner.

![08-api-folder-structure.jpg](https://dev-to-uploads.s3.amazonaws.com/i/8tpket3dljyi0wajzkuf.jpg)

# `README`

`<migration>/README.md` is a human-readable description of the migration.

![09-database-migration-initialize-database.jpg](https://dev-to-uploads.s3.amazonaws.com/i/919d2z0ex8zw77j3sja6.jpg)

Includes metadata like:
* when the migration was created and by who
* a list of the actual migration changes
* a diff of the changes that are made to the `schema.prisma` file

![10-database-changes](https://dev-to-uploads.s3.amazonaws.com/i/3rhekltrx73wcscbuzah.jpg)

`<migration>/schema.prisma` is the schema that will be created if the migration is applied to the project.

![11-schema-prisma-migration.jpg](https://dev-to-uploads.s3.amazonaws.com/i/2g8xewy97q1gd29m9l0o.jpg)

It looks like TypeScript is yelling at us because according to the Prisma docs before using the [`migrate up` command you must define a valid `datasource` within your schema.prisma file](https://www.prisma.io/docs/reference/tools-and-interfaces/prisma-cli/command-reference#migrate-up).

For example the url could be set to `file:my-database.db` to define a SQLite database file within the current directory. Prisma's migration functionality is currently in an experimental state.

# `steps.json`

`steps.json` is an alternative representation of the migration steps that will be applied.

![12-steps-json.jpg](https://dev-to-uploads.s3.amazonaws.com/i/nlu2dmpzvfk9qjx5rw4d.jpg)

Steps are actions that resolve into zero or more database commands. Steps generically describe models, fields and relationships, so they can be easily translated to datasource-specific migration commands.

# `db up`

Generates the Prisma client and applies migrations. [`migrate up`](https://www.prisma.io/docs/reference/tools-and-interfaces/prisma-cli/command-reference#migrate-up) migrates the database up to a specific state.

![13-yarn-redwood-db-up](https://dev-to-uploads.s3.amazonaws.com/i/zilmcvz5eubgavyhh0x8.jpg)

This will apply the migration. It will run the commands against the database to create the changes we need. This results in creating a new table called `Post` with the fields we previously defined.

![14-migrate-database-up-started](https://dev-to-uploads.s3.amazonaws.com/i/n5zz1eh33q84wi84qg94.jpg)

The following `datasource` defines a SQLite database.

![15-datamodel-that-will-initialize-the-db](https://dev-to-uploads.s3.amazonaws.com/i/ks7ary9dej93nfohsxu6.jpg)

![16-database-migration](https://dev-to-uploads.s3.amazonaws.com/i/gge1uqjuu0c247i6g9xi.jpg)

![17-generating-prisma-client](https://dev-to-uploads.s3.amazonaws.com/i/f7hz8wtp11hkr65fyd11.jpg)

# `generate scaffold`

Generate Pages, SDL, and Services files based on a given DB schema Model. Also accepts `<path/model>`.

![18-yarn-redwood-g-scaffold-post](https://dev-to-uploads.s3.amazonaws.com/i/hejunjalusimfqc0ni7j.jpg)

A scaffold quickly creates a CRUD for a model by generating the following files and corresponding routes:
* sdl
* service
* layout
* pages
* cells
* components

![19-generating-scaffold-files](https://dev-to-uploads.s3.amazonaws.com/i/uxpifwyj51wv1oris5f1.jpg)

Lets open our browsers and enter `localhost:8910/posts`.

![20-posts-page](https://dev-to-uploads.s3.amazonaws.com/i/57122pye2dznq6afq1l6.jpg)

We have a new page called Posts with a button to create a new post. If we click the new post button we are given an input form with fields for title and body.

![21-new-post-form](https://dev-to-uploads.s3.amazonaws.com/i/u7xmgfa9essbyxnbleqn.jpg)

We were taken to a new route, `/posts/new`. Let's create a blog post about everyone's favorite dinosaur.

![22-new-deno-post](https://dev-to-uploads.s3.amazonaws.com/i/xesdkrsz41e62l8n2wla.jpg)

If we click the save button we are brought back to the posts page.

![23-deno-post-created](https://dev-to-uploads.s3.amazonaws.com/i/1kpfuu8yzr4enme5ksq9.jpg)

We now have a table with our first post.

![24-deno-post-edit](https://dev-to-uploads.s3.amazonaws.com/i/5960uw4sxoognkym6t82.jpg)

When we click the edit button we are taken to a route for the individual post that we want to edit. Each post has a unique id.

![25-deno-post-edited](https://dev-to-uploads.s3.amazonaws.com/i/6p5pdukj78eq9db09mon.jpg)

The title has now been changed from `01-deno` to `01-deno-edit`.

![26-will-delete-post](https://dev-to-uploads.s3.amazonaws.com/i/5ou2sj12nfeqx5skyai6.jpg)

Lets create another post.

![27-hover-delete-button](https://dev-to-uploads.s3.amazonaws.com/i/ry7es7pt0u57pbd8kx4x.jpg)

If we click the delete button we will be given a warning.

![28-delete-post-warning](https://dev-to-uploads.s3.amazonaws.com/i/2e6nm9qhipmd9wa8iiqu.jpg)

Click ok to confirm and you'll receive a message saying your post has been deleted.

![29-post-deleted](https://dev-to-uploads.s3.amazonaws.com/i/o7nhmnk6h8iqbbcfvi9x.jpg)

Lets add another blog post:

![31-fauna-post](https://dev-to-uploads.s3.amazonaws.com/i/9er8hp0hmqcf75xryjrs.jpg)

And one more:

![32-next-post](https://dev-to-uploads.s3.amazonaws.com/i/snl7cab45hr3xivh7ast.jpg)

If we make more posts they will start on the id after the deleted item. We already had an id 2. You can't call something else id 2, that would make your database a liar. I created and deleted one more post before continuing on, so that's why I am missing id 2 and id 3.

![30-most-posts](https://dev-to-uploads.s3.amazonaws.com/i/t99kca9pv79kp39bk6v6.jpg)

In the [next part](https://dev.to/ajcwebdev/a-first-look-at-redwood-js-part-4-2m0g) we'll look at the code that powers this functionality and learn about [Cells](https://redwoodjs.com/tutorial/cells). We'll also set up our frontend to query data from our backend to render a list of our blog posts to the front page.

# Part 4 - CRUD

> *What I’ve experienced and what I know many people have experienced learning React and getting into this is that path right now is very, very, very, very, very long. And hard. And horrible.*  
>
>***Tom Preston-Werner***
>***[Full Stack Radio 138](https://www.fullstackradio.com/episodes/138)***

In [part 1](https://dev.to/ajcwebdev/a-first-look-at-redwood-js-1017) we installed and created our first RedwoodJS application, in [part 2](https://dev.to/ajcwebdev/a-first-look-at-redwood-js-part-2-44ph) we created links to our different page routes and a reusable layout for our site, and in [part 3](https://dev.to/ajcwebdev/a-first-look-at-redwood-js-part-3-5ao5) we got our database up and running and learned to create, retrieve, update, and destroy blog posts.

In this part we'll look at all the code that was generated that allowed us to perform our CRUD operations on the blog posts. We'll also set up our frontend to query data from our backend to render a list of our blog posts to the front page. If you've never worked with [GraphQL](https://www.howtographql.com/) or serverless functions like [Lambda](https://www.serverless.com/aws-lambda/) then some of the concepts in this part may be new.

If you want to learn more I have a post about [the history of GraphQL, current projects, and resources](https://dev.to/ajcwebdev/a-short-history-of-graphql-20nb).

# `api/src`

We've seen the `prisma` folder under `api`, now we'll look at the `src` folder containing our GraphQL code. Redwood comes with GraphQL integration built in to make it easy to get our client talking to our serverless functions.

![01-api-src-folder](https://dev-to-uploads.s3.amazonaws.com/i/p4fn5syh1i8ruaknq2mx.jpg)

# `api/src/functions`

The `functions` folder will contain any lambda functions your app needs in addition to the `graphql.js` file auto-generated by Redwood.

![02-api-src-functions-folder](https://dev-to-uploads.s3.amazonaws.com/i/vwnsj9ofwozsqpdyz57h.jpg)

# `graphql.js`

This file is required to use the GraphQL API.

![03-api-src-functions-graphql](https://dev-to-uploads.s3.amazonaws.com/i/vv2tq8i55o013gk6ojqn.jpg)

Don't worry too much about what's going on in this file, we will be working more with the schema definition language.

# SDL: Schema Definition Language

`graphql` contains your GraphQL schema and is written in a Schema Definition Language. The files will end in `.sdl.js`.

![04-api-src-graphql-folder](https://dev-to-uploads.s3.amazonaws.com/i/zxqkpem39z40ao7mnp9x.jpg)

# `posts.sdl.js`

GraphQL schemas for a service are specified using the GraphQL SDL ([schema definition language](https://graphql.org/learn/schema/)) which defines the API interface for the client. Our `schema` has five object types each with their own fields and types.

![05-api-src-graphql-posts-sdl
](https://dev-to-uploads.s3.amazonaws.com/i/5o4we1jhx17lh4j8efmz.jpg)

## `Post`
Represents a blog post

![06-api-src-graphql-posts-sdl-Post](https://dev-to-uploads.s3.amazonaws.com/i/4kay4muxjejve35nib3u.jpg)

## `Query`
Represents a query that retrieves either:
* multiple posts in an array (line 12)
* a single post with an `id` (line 13)

![07-api-src-graphql-posts-sdl-Query](https://dev-to-uploads.s3.amazonaws.com/i/1zvdg4j316xsj25etds9.jpg)

## `CreatePostInput`
Represents `title` and `body` of a new post

![08-api-src-graphql-posts-sdl-CreatePostInput](https://dev-to-uploads.s3.amazonaws.com/i/qc5tl58xc297sii3m5xf.jpg)

## `UpdatePostInput`
Represents `title` and `body` of a post being updated

![09-api-src-graphql-posts-sdl-UpdatePostInput](https://dev-to-uploads.s3.amazonaws.com/i/7fvwnfwnk7ertm6hnwtb.jpg)

## `Mutation`
Represents create, update, and delete operations on a post

![10-api-src-graphql-posts-sdl-Mutation](https://dev-to-uploads.s3.amazonaws.com/i/ptzrabxzayuj3xvfledx.jpg)

* `createPost`: Takes `title` and `body` from `CreatePostInput` and creates a `Post`

* `updatePost`: Takes `title` and `body` from `UpdatePostInput` and `id` of the `Post` being updated

* `deletePost`: Takes `id` of the `Post` being deleted

# `lib`

`lib` contains one file, `db.js`, which instantiates the Prisma database client. You can use this folder for other code related to the API side that doesn't fit in functions or services.

![11-api-src-lib-folder](https://dev-to-uploads.s3.amazonaws.com/i/rlzrocgjoyc402cmnkn3.jpg)

# `db.js`

[Prisma Client](https://www.prisma.io/docs/reference/tools-and-interfaces/prisma-client) is an auto-generated and type-safe query builder that's tailored to your data.

![12-api-src-lib-db](https://dev-to-uploads.s3.amazonaws.com/i/ay5ibk7uzeh0rz85pc8a.jpg)

# `services`

`services` contains business logic related to your data. When you're querying or mutating data for GraphQL, that code ends up here, but in a format that's reusable in other places in your application. A service implements the logic of talking to the third-party API.

![13-api-src-services-folder](https://dev-to-uploads.s3.amazonaws.com/i/3pwaj3wamgtnbl8iqugd.jpg)

Redwood will automatically import and map resolvers from the `services` file onto your SDL. You write resolvers in a way that makes them easy to call as regular functions from other [resolvers](https://www.softwaredaily.com/topic/graphql/question/5ebcfe42ab37a6002da0d63e) or `services`.

![14-api-src-services-posts](https://dev-to-uploads.s3.amazonaws.com/i/5875tb982w1poimunt5t.jpg)

Redwood will look in `api/src/services/posts/posts.js` for the following five resolvers:

### `posts()`
![14-1-api-src-services-posts-posts](https://dev-to-uploads.s3.amazonaws.com/i/d9us71jk32gdm3607r28.jpg)

### `post({id})`
![14-2-api-src-services-posts-post](https://dev-to-uploads.s3.amazonaws.com/i/5itfxp1tf66h8ylll6az.jpg)

### `createPost({input})`
![14-3-api-src-services-posts-createPost](https://dev-to-uploads.s3.amazonaws.com/i/tr0hh0rift9muttjo8cp.jpg)

### `updatePost({id, input})`
![14-4-api-src-services-posts-updatePost](https://dev-to-uploads.s3.amazonaws.com/i/zj83x56uh09253wf2izk.jpg)

### `deletePost({id})`
![14-5-api-src-services-posts-deletePost](https://dev-to-uploads.s3.amazonaws.com/i/gjalgcswunobtewv317d.jpg)

# `PostPage`

`PostPage` is a component that takes in `PostCell` with a post's `id` as a prop. `PostCell` is wrapped in the `PostsLayout` component.

![15-web-src-pages-PostPage](https://dev-to-uploads.s3.amazonaws.com/i/28pioylp3oqk6no3s42c.jpg)

Here's the view of `PostPage` with a `PostCell` wrapped in the `PostsLayout`:

![16-PostPage-rendered](https://dev-to-uploads.s3.amazonaws.com/i/ytvwsrqml2t7t6nqp6eo.jpg)

# `PostsLayout`

![17-layouts-PostsLayout](https://dev-to-uploads.s3.amazonaws.com/i/xumxuzi89chjjrb9tbvn.jpg)

If you click Posts you will be linked to `routes.posts()` and if you click New Post you will be linked to `routes.NewPost()` 

Here's the view of just the `PostsLayout`:

![18-PostsLayout-rendered](https://dev-to-uploads.s3.amazonaws.com/i/h4kubdnasvfwtxce4p38.jpg)

# `PostCell`

Cells provide a simpler and more declarative approach to data fetching. When you create a cell you export several specially named constants and then Redwood takes it from there.

Cells should be used when your component needs some data from the database or other service that is delayed in responding. Redwood juggles what is displayed and when.

![19-web-src-components-PostCell](https://dev-to-uploads.s3.amazonaws.com/i/zhdb77u4h5qzkpy4ghbv.jpg)

The minimum you need for a cell are the `QUERY` and `Success` exports.
* If you don't export an `Empty` component, empty results will be sent to your `Success` component.
* If you don't provide a `Failure` component you'll get error output sent to the console.

# `Post`

* [`useFlash`](https://redwoodjs.com/docs/flash-messaging-bus.html#useflash-hook) is an abridgment of `React.useContext(FlashContext)`.
* [`useMutation`](https://www.apollographql.com/docs/react/data/mutations/) is a hook provided by Apollo which will allow us to execute the mutation when we're ready. It is the primary API for executing mutations in an Apollo application.

![20-web-src-components-Post](https://dev-to-uploads.s3.amazonaws.com/i/6b8o02fiad235wki946j.jpg)

## `DELETE_POST_MUTATION`
GraphQL string representing the mutation that is passed into `useMutation`

![21-web-src-components-Post-DELETE_POST_MUTATION](https://dev-to-uploads.s3.amazonaws.com/i/5h3ob2a6dj9u51j836pw.jpg)

## `onCompleted`

![22-web-src-components-Post-onCompleted](https://dev-to-uploads.s3.amazonaws.com/i/efcnlcx4sy93met5vqly.jpg)

Displays a message letting you know the post has been deleted

![22-1-web-src-components-Post-onCompleted-rendered](https://dev-to-uploads.s3.amazonaws.com/i/o6fgt8algt5f2ochy79q.jpg)

## `onDeleteClick`

![23-web-src-components-Post-onDeleteClick](https://dev-to-uploads.s3.amazonaws.com/i/tlur271kq4temva6o2ru.jpg)

Asks you to confirm that you are sure you want to delete the post, and gives the `id` of the post about to be deleted

![23-1-web-src-components-Post-onDeleteClick-rendered](https://dev-to-uploads.s3.amazonaws.com/i/5yxnc2r858800cf73y5n.jpg)

# `rw-segment`

In the return statement of the `Post` component there is a `<div>` with the className `rw-segment` which takes the `post` object and pulls out the post's `id`, `title`, `body`, and `createdAt` date.

![24-web-src-components-Post-rw-segment](https://dev-to-uploads.s3.amazonaws.com/i/uampof3jlrwtx4pgqdvq.jpg)

Here's the view in our application:

![25-Post-rw-segment-rendered](https://dev-to-uploads.s3.amazonaws.com/i/ocetrswbe7ih41x7pwud.jpg)

# `rw-button-group`

This code corresponds to the edit and delete buttons.

![26-web-src-components-Post-rw-button-group](https://dev-to-uploads.s3.amazonaws.com/i/8s5309g282e1ar0pxulm.jpg)

Here's the view in our application:

![27-Post-rw-button-group-rendered](https://dev-to-uploads.s3.amazonaws.com/i/p4kra1j13aojdsp53reb.jpg)

Now if we look at the entire component we can see how `rw-segment` and `rw-button-group` are nested inside empty tags.

![28-web-src-components-Post-return](https://dev-to-uploads.s3.amazonaws.com/i/mqshax5qboz32eaf0f6l.jpg)

Here's the view for the entire component.

![29-Post-return-rendered](https://dev-to-uploads.s3.amazonaws.com/i/vkyu2uod0pufu5mcdf5f.jpg)

# `NewPostPage`

`NewPostPage` is a component that takes in `NewPost` wrapped in the `PostsLayout` component. The same `PostsLayout` from `PostPage` is being reused here but with a different component nested inside.

![30-web-src-pages-NewPostPage](https://dev-to-uploads.s3.amazonaws.com/i/3d4iwj8nylkk0hgb5ckb.jpg)

Here's the view:

![31-NewPostPage-rendered](https://dev-to-uploads.s3.amazonaws.com/i/gn3ld4u3r3aeyutjvryx.jpg)

# `NewPost`

`NewPost` is a component that takes in data from the `PostForm` component and uses `CREATE_POST_MUTATION` to save the post to the database.

![32-web-src-components-NewPost](https://dev-to-uploads.s3.amazonaws.com/i/e8r7kn63op9wuvic3ewv.jpg)

Here's the view:

![33-new-post-form-rendered](https://dev-to-uploads.s3.amazonaws.com/i/l7mqsdjpj68lqaqtkqua.jpg)

# `PostForm`

Redwood provides several helpers to make your life easier when working with forms. It is a wrapper around [react-hook-form](https://react-hook-form.com/).

![34-src-components-PostForm](https://dev-to-uploads.s3.amazonaws.com/i/63mf8q41ms8zmvmkdpg6.jpg)

# `onSubmit`

A prop that accepts a function name or anonymous function to be called if validation is successful. Behind the scenes the handler given to `onSubmit` is given to react-hook-form's [`handleSubmit`](https://react-hook-form.com/api/#handleSubmit) function.

![35-src-components-PostForm-onSubmit](https://dev-to-uploads.s3.amazonaws.com/i/pxb2jzewpip02t3892zg.jpg)

# `<Form>`

Surrounds all form elements and provides contexts for errors and form submission.

![36-src-components-PostForm](https://dev-to-uploads.s3.amazonaws.com/i/u9p64kiu714rywymuxfk.jpg)

# `<FormError>`

Displays an error message, typically at the top of your form, containing error messages from the server

![37-src-components-PostForm-FormError](https://dev-to-uploads.s3.amazonaws.com/i/kopxz4rajuith88cvq7w.jpg)

# `<Label>`

Used in place of the HTML `<label>` tag and can respond to errors with different styling

![38-src-components-PostForm-Title-Label](https://dev-to-uploads.s3.amazonaws.com/i/q2owaav8w3vdqup8pq4o.jpg)

# `<TextField>`

Renders an HTML <input type="text"> field, but is registered with react-hook-form to provide some validation and error handling.

![39-src-components-PostForm-Title-TextField](https://dev-to-uploads.s3.amazonaws.com/i/yyiscrr4pk5zdtwl8ktw.jpg)

# `<FieldError>`

Displays form validation errors and server errors.

![40-src-components-PostForm-Title-FieldError](https://dev-to-uploads.s3.amazonaws.com/i/9vrhbi9fb8p85th2yump.jpg)

Here's the view:

![41-Title-rendered](https://dev-to-uploads.s3.amazonaws.com/i/ei6pkhkp0ftu1nlomkxy.jpg)

`<Label>`, `<TextField>`, and `<FieldError>` are also used for the Body.

![42-Body](https://dev-to-uploads.s3.amazonaws.com/i/rvmxv1baq5toyi7ia4pg.jpg)

Here's the view:

![43-Body-rendered](https://dev-to-uploads.s3.amazonaws.com/i/w3tkymddbblwioxawp4i.jpg)

# `<Submit>`

Used in place of `<button type="submit">` and will trigger a validation check and "submission" of the form. It executes the function given to the `onSubmit` attribute on `<Form>`.

![44-Save](https://dev-to-uploads.s3.amazonaws.com/i/yftnmrnnvh7wu2w6smnx.jpg)

Here's the view:

![45-Save-rendered](https://dev-to-uploads.s3.amazonaws.com/i/vjpc0o4riipmg0yr3pbm.jpg)

And here's the view of the entire `<Form>` component:

![46-PostForm-rendered](https://dev-to-uploads.s3.amazonaws.com/i/3v46mdwsvorcd1gqosim.jpg)

# `EditPostPage`

Much like `PostPage`, `EditPostPage` is a component that takes in `EditPostCell` with a post's `id` as a prop. `EditPostCell` is wrapped in the `PostsLayout` component.

![47-web-src-pages-EditPostPage](https://dev-to-uploads.s3.amazonaws.com/i/wv7r7ll0k1vkx970m7d2.jpg)

Here's the view:

![48-EditPostPage-rendered](https://dev-to-uploads.s3.amazonaws.com/i/wmzu2lgzbv2aoatffa2o.jpg)

# `EditPostCell`

We have the `UPDATE_POST_MUTATION` and `QUERY` object types we discussed at the beginning of this article. At the bottom we are again returning the `<PostForm>` component except this time we also have a `post` prop to specify which post is being edited.

![49-web-src-components-EditPostCell](https://dev-to-uploads.s3.amazonaws.com/i/vhut3tz01l71dl3jwn96.jpg)

Here's the view:

![50-EditPostCell-rendered](https://dev-to-uploads.s3.amazonaws.com/i/qdiz1vubwwdf27ivtnif.jpg)

# `PostsPage`

In Redwood we use singular "post" when working with a single post object and the data associated with it. When we are working with many posts we use the plural "posts." Here we are displaying all of our posts, so it's called `PostsPage`.

![51-web-src-pages-PostsPage](https://dev-to-uploads.s3.amazonaws.com/i/lnfmzpy7q4ukr3uoqgrx.jpg)

Here's the view:

![52-PostsPage-rendered](https://dev-to-uploads.s3.amazonaws.com/i/7wzcdzu69xwsgus2d1r2.jpg)

# `PostsCell`

![53-web-src-components-PostsCell](https://dev-to-uploads.s3.amazonaws.com/i/kjgnfqrdujdyrq3vuvj2.jpg)

Here's the view if you have no posts:

![54-posts-page](https://dev-to-uploads.s3.amazonaws.com/i/amyxsy9qenzoh3o2q8co.jpg)

# `Posts`

![55-web-src-components-Posts](https://dev-to-uploads.s3.amazonaws.com/i/snm1sfn10k3zuvwi9nr2.jpg)

`truncate` limits the length of the posts being shown, and `timeTag` encapsulates the logic for created a timestamp for each post.

![56-web-src-components-Posts-PostsList](https://dev-to-uploads.s3.amazonaws.com/i/juwt14splx7gtt33bkus.jpg)

`onCompleted` and `onDeleteClick` are the same functions that we saw in the `NewPost` component.

# `rw-table-wrapper-responsive`

We have a `div` that wraps one big table with the className `rw-table`.

![57-web-src-components-Posts-return](https://dev-to-uploads.s3.amazonaws.com/i/8wzutcd2fkxjhp73quj6.jpg)

Here's the view:

![58-Posts-rw-table-wrapper-responsive-rendered](https://dev-to-uploads.s3.amazonaws.com/i/o1f2pi8mxmzxmsj86hb7.jpg)

This is a lot of code so we'll break this down to the table head and table body, and the table body is broken down into table posts and table actions.
1. Table head (47-55)
2. Table body (56-91)
3. Table posts (57-62)
4. Table actions (63-88)

![59-Posts-rw-table-wrapper-responsive](https://dev-to-uploads.s3.amazonaws.com/i/8xgl6k2x92s2lstwdi3f.jpg)

# `<thead>`

The table head lets us know the different fields.

![60-Posts-thead](https://dev-to-uploads.s3.amazonaws.com/i/lwnqvinu625el0rkjcb8.jpg)

Here's the view:

![61-Posts-thead-rendered](https://dev-to-uploads.s3.amazonaws.com/i/glbmk5wznlufgel4t4z1.jpg)

# `<tbody>`

In the first half of the table body we map over the data passed through the `post` prop, use the post's `id` for the `key` and then pull out the `id`, `title`, `body`, and `createdAt` time.

![62-Posts-td](https://dev-to-uploads.s3.amazonaws.com/i/i47ffyvrkd8ozjv162io.jpg)

Here's the view:

![63-Posts-td-rendered](https://dev-to-uploads.s3.amazonaws.com/i/11wn58igymraxfee2li3.jpg)

In the second half of the table body we have links to go to a post's page, edit a post, or delete a post.

![64-Posts-rw-table-actions](https://dev-to-uploads.s3.amazonaws.com/i/jz3rfn88x9igohxo412u.jpg)

Here's the view:

![65-Posts-rw-table-actions-rendered](https://dev-to-uploads.s3.amazonaws.com/i/834jvs58ynt6vz1exwou.jpg)

# `generate cell`

Now we are going to create a cell that will render the most recent blog posts to the front page.

![66-yarn-redwood-generate-cell-BlogPosts](https://dev-to-uploads.s3.amazonaws.com/i/yzdzjfaayztr9b5t5180.jpg)

Redwood will generate a file called `BlogPostsCell.js` and a file for testing called `BlogPostsCell.test.js`.

![67-generating-cell-files](https://dev-to-uploads.s3.amazonaws.com/i/2ica696wtl6kl0q04udn.jpg)

This will generate a `QUERY` for us and use `JSON.stringify` to render the results of the query. But there is one thing we need to change.

![68-web-src-components-BlogPostsCell](https://dev-to-uploads.s3.amazonaws.com/i/4xircas45g7ws73y4fp9.jpg)

We need to make a slight adjustment to get our QUERY to match up with the schema that we have already created. Change `blogPosts` on lines 3, 15, 16 to just `posts`.

![69-web-src-components-BlogPostsCell-posts-edit](https://dev-to-uploads.s3.amazonaws.com/i/phubewo9nep40b98v08s.jpg)

Now we can take the `BlogPostsCell` component and insert it into our `HomePage` component. We need to first import it, and then place the tag inside of the `BlogLayout` tags.

![70-BlogPostsCell-in-HomePage](https://dev-to-uploads.s3.amazonaws.com/i/joyk0mneceqc4qsn63dn.jpg)

This gives us just the `id` and the `typename` which is `Post`.

![71-BlogPostsCell-render-HomePage](https://dev-to-uploads.s3.amazonaws.com/i/ysnrohoraf25ul47iw22.jpg)

Lets go back to our `QUERY` and add in `title`, `body`, and `createdAt`.

![72-web-src-components-BlogPostsCell-id-title-body-createdAt](https://dev-to-uploads.s3.amazonaws.com/i/r2gi8723ql9tjlgkxyro.jpg)

Now we should get all the info we need on the home page.

![73-BlogPostsCell-render-id-title-body-createdAt](https://dev-to-uploads.s3.amazonaws.com/i/s7fsmj90nm6j0m0ir2h5.jpg)

This doesn't look very good though, I don't think anyone would want to read this blog. In the `BlogPostsCell` file inside `Success` we can create a component for our posts and give it a little structure.

![74-BlogPostsCell-map-over-posts](https://dev-to-uploads.s3.amazonaws.com/i/3kb5ndh5vxfaodu5kfv0.jpg)

We'll do some more styling later on but for now we have our posts rendered to the front page.

![75-BlogPostsCell-render-map-over-posts](https://dev-to-uploads.s3.amazonaws.com/i/4nion84xg9lco3guqomu.jpg)

In the next part we'll create a contact form.


# Part 5 - Contact

> *We see it as a Rails replacement. Anything you would normally do with Rails we hope that you’ll be able to do with Redwood.*  
>
>***Tom Preston-Werner***
>***[Full Stack Radio 138](https://www.fullstackradio.com/episodes/138)***

If you've made it this far into my series of blog posts I commend you and hope you've found them useful.

In [part 1](https://dev.to/ajcwebdev/a-first-look-at-redwood-js-1017) we created our RedwoodJS app, in [part 2](https://dev.to/ajcwebdev/a-first-look-at-redwood-js-part-2-44ph) we created links between different pages and a reusable layout, in [part 3](https://dev.to/ajcwebdev/a-first-look-at-redwood-js-part-3-5ao5) we got the database up and running and learned CRUD operations for our blog posts, and in [part 4](https://dev.to/ajcwebdev/a-first-look-at-redwood-js-part-4-2m0g) we set up the frontend to query data from the backend to render a list of blog posts to the front page.

In this part we'll be combining everything we've learned up to this point to generate a contact page and take input from a user. We'll be using the same form tags that we learned about in part 4, which are wrappers around [react-hook-form](https://react-hook-form.com/get-started).

This is the simplest way to create a form, but Redwood can be used with other popular React form libraries like Formik or you can use react-hook-form directly.

Forms are a topic I'm particularly passionate about and believe receive far too little attention in bootcamp curriculums and online tutorials. They may not be the most exciting topic, but I encourage you to not gloss over these parts of the framework.

# `generate page`

The first step is to enter the `yarn redwood generate page` command to create our contact page.

![01-yarn-redwood-generate-page-contact](https://dev-to-uploads.s3.amazonaws.com/i/gnky2rp1tjrwr13qfokx.jpg)

This same command could be shorted to `yarn rw g page`.

![02-generating-page-files](https://dev-to-uploads.s3.amazonaws.com/i/uwwn9tlak4c6efgcpr7b.jpg)

# `web/src/pages/ContactPage`

This generates a folder called `ContactPage` in our `web/src/pages` folder, and creates two files, `ContactPage.js` and `ContactPage.test.js`.

![03-pages-folder](https://dev-to-uploads.s3.amazonaws.com/i/oqifajbebykifbtn4b97.jpg)

This should look familiar if you've followed along with the whole series.

# `ContactPage.js`

![04-ContactPage](https://dev-to-uploads.s3.amazonaws.com/i/t0tnp2nnh789f9w36d67.jpg)

Our `ContactPage` component contains the same boilerplate we saw when we created our home page and our about page.

![05-ContactPage-rendered](https://dev-to-uploads.s3.amazonaws.com/i/rca3x88upx0ygw2rtgjo.jpg)

Lets go to our BlogLayout and add a link to the contact page.

![06-routes.contact](https://dev-to-uploads.s3.amazonaws.com/i/pqpeyfrojltroi1b7gu7.jpg)

Now we'll import `BlogLayout` into `ContactPage.js` and wrap our contact page content in the `BlogLayout` component.

![07-ContactPage-BlogLayout](https://dev-to-uploads.s3.amazonaws.com/i/jn2jhta2c7y4b39bm7vf.jpg)

We can now navigate to any of our three pages.

![08-ContactPage-BlogLayout-rendered](https://dev-to-uploads.s3.amazonaws.com/i/ghcflmtowr04qa52pybq.jpg)

We're going to import the `Form` tags that we looked at in the previous section. Refer to [part 4](https://dev.to/ajcwebdev/a-first-look-at-redwood-js-part-4-2m0g) or the [Redwoodjs docs](https://redwoodjs.com/docs/form) to learn more about these tags.

![09-ContactPage-Form-imports](https://dev-to-uploads.s3.amazonaws.com/i/31uifks0kpj1cewv9qnt.jpg)

Now that we've imported them lets create a `Form` with a `Label` and `TextField` for name, and a `Submit` button.

![10-ContactPage-Form-Label-TextField-Submit](https://dev-to-uploads.s3.amazonaws.com/i/5l2goqr45sb3yin4ee0z.jpg)

Here is the label, input, and button.

![11-ContactPage-Form-rendered](https://dev-to-uploads.s3.amazonaws.com/i/xgrnf2eo0iw84s19rpda.jpg)

We'll add a little CSS in a moment, but first lets see what happens if we try to input data.

![12-ContactPage-input](https://dev-to-uploads.s3.amazonaws.com/i/uq14xbl4dtr0w742eicp.jpg)

If we click the save button we'll get an error.

![13-error-message](https://dev-to-uploads.s3.amazonaws.com/i/hb4gmxc86wcmdtuzhiy2.jpg)

This makes sense, we haven't told our form what to do yet with the data. Let's create a function called `onSubmit` that will take in a `data` object and console log the `data` object.

![14-ContactPage-onSubmit](https://dev-to-uploads.s3.amazonaws.com/i/7sny4ozuquipsgnb79fr.jpg)

The `onSubmit` prop accepts a function name or anonymous function to be called if validation is successful. This function will be called with a single object containing key/value pairs of all Redwood form helper fields in your form.

![15-ContactPage-Form-onSubmit](https://dev-to-uploads.s3.amazonaws.com/i/gtmct9loe4l157euyu9z.jpg)

Now if enter data into the form and click save we'll see the following in our console:

![16-console.log(data)](https://dev-to-uploads.s3.amazonaws.com/i/1kh371fa5okutqyast5q.jpg)

Our input is contained in the `data` object. Right now it only has a key/value pair for name but we'll be adding more in a moment. But before doing that lets see what we can do with this `data` object.

![17-ContactPage-onSubmit-data.name](https://dev-to-uploads.s3.amazonaws.com/i/9gd75g46o52c32wz5y6i.jpg)

We can pull out the value of name by console logging `data.name`:

![18-console.log(data.name)](https://dev-to-uploads.s3.amazonaws.com/i/tejm0ez4iagkibw6tgfc.jpg)

We want to be able to accept a longer message from our users, so we're going to import the `TextAreaField` tag.

![19-ContactPage-TextAreaField-import](https://dev-to-uploads.s3.amazonaws.com/i/3dmk4lpgjfi0g2k6ax7w.jpg)

We now how a `TextField` for name and email, and a `TextAreaField` for a message.

![20-ContactPage-email-message](https://dev-to-uploads.s3.amazonaws.com/i/7sl845kphfn7u77ger1b.jpg)

To make this look a little nicer we're going to include just a little CSS.

![21-index.css](https://dev-to-uploads.s3.amazonaws.com/i/wuw2gdiimpwb69h2tyct.jpg)

Our buttons, inputs, and labels are now `display: block` which adds a line break after any appearance of these tags, and the label also has a little bit of margin on the top.

![22-ContactPage-email-message-rendered](https://dev-to-uploads.s3.amazonaws.com/i/aez5p7kwdg9bmu2qkaet.jpg)

Lets test out all the fields.

![23-ContactPage-email-message-input](https://dev-to-uploads.s3.amazonaws.com/i/ij9nzr2f3mzklww3okab.jpg)

We now are getting back an object with 3 key/value pairs.

![24-ContactPage-email-message-console.log](https://dev-to-uploads.s3.amazonaws.com/i/j0l66t5v4dg5ts0wreuv.jpg)

We can console log any part of the object that we want.

![25-data.email-data.message](https://dev-to-uploads.s3.amazonaws.com/i/w0aaeha6su8ppez2rwfl.jpg)

Now if we look at our console we'll see each output and it even tells us which file and line corresponds to each piece of data.

![26-data.email-data.message-console.log](https://dev-to-uploads.s3.amazonaws.com/i/k2a1l3wgl38h2j3imv40.jpg)

What happens if we only fill out some of the form and try to submit?

![27-just-name-input](https://dev-to-uploads.s3.amazonaws.com/i/l15pcrt8vroptzujvjts.jpg)

The form doesn't care, it simply takes the empty inputs and returns an empty string.

![28-empty-email-message](https://dev-to-uploads.s3.amazonaws.com/i/i8u3bizp271soc4yo5u0.jpg)

Lets add some validation so the user can't submit the form unless they've given input for all three fields.

![29-errorClassName-validation](https://dev-to-uploads.s3.amazonaws.com/i/wb59lwmmwu4fcb840alq.jpg)

We gave each `TextField` an `errorClassName` with the attribute `error`. The `validation` prop accepts an object containing options for react-hook-form. Right now we're just adding the `required` attribute, but later we'll use the `validation` prop for a regular expression.

![30-input.error-textarea.error-label.error](https://dev-to-uploads.s3.amazonaws.com/i/d64m79tnai9smdypvjpo.jpg)

In our CSS we'll add the following properties for errors.

![31-textfield-errors](https://dev-to-uploads.s3.amazonaws.com/i/ievk6oz92vhx7xo10r6x.jpg)

Now when we try to submit an empty field we see the color change to red.

![32-textfield-errors-with-name](https://dev-to-uploads.s3.amazonaws.com/i/xk6otdf9nfbterim9jth.jpg)

Once we give input the red error color goes away.

![33-invalid-email](https://dev-to-uploads.s3.amazonaws.com/i/ahq77s6l4vck30leeoku.jpg)

There's still an issue, which is we can submit an email that is invalid.

![34-email-regex](https://dev-to-uploads.s3.amazonaws.com/i/tyo3m4a64famwe53ybcf.jpg)

Here's a regular expression provided in the Redwood tutorial video. Don't ask me to explain it, cause I don't know what it's doing. All I know is it does a thing with the `@` symbol, then it does another thing with the `.` symbol, then it does some other things and figures out if you gave an email or not. Google "regex tutorials" if that wasn't a satisfactory explanation for you. 

![35-email-error](https://dev-to-uploads.s3.amazonaws.com/i/8767bg0540xoric7emeh.jpg)

Now we get an error if we don't provide a valid email address. It would really be nice if we could tell our user why they are getting an error.

![36-import-FieldError](https://dev-to-uploads.s3.amazonaws.com/i/k94z8brdv9579rren5jt.jpg)

We're going to import `FieldError` to show error messages to our users.

![37-FieldError-name-email-message](https://dev-to-uploads.s3.amazonaws.com/i/nanx830w4mi64lnt5wlx.jpg)

Now if we try to submit without giving input we are told that the field is required.

![38-name-email-message-required](https://dev-to-uploads.s3.amazonaws.com/i/ru2fv4gbj42b8z2zi6y2.jpg)

If we enter an invalid email we are told that the email is not formatted correctly.

![39-email-formatted-incorrectly](https://dev-to-uploads.s3.amazonaws.com/i/8m3vz5y783ig4jn7q2fi.jpg)

If we add the `errorClassName` to the `Label` tags we'll also turn the labels red if there's an error.

![40-label-errorClassName](https://dev-to-uploads.s3.amazonaws.com/i/toesfu3e17p12qept4nf.jpg)

Now we have the label and the input field turn red if there's an error.

![41-label-errors](https://dev-to-uploads.s3.amazonaws.com/i/xh9903231ih17rtema60.jpg)

Might as well make everything red while we're at it.

![42-FieldError-style-red](https://dev-to-uploads.s3.amazonaws.com/i/74710e4qxk9vn66gftl8.jpg)

Since the `FieldError` will only show on errors we can just inline styles with `style={{ color: 'red' }}`.

![43-all-red](https://dev-to-uploads.s3.amazonaws.com/i/k94wcphsoe2jcqakb8xv.jpg)

Glorious red as far as the eye can see. Something's still not right though. Lets get "message is required" onto it's own line.

![44-message-error-display-block](https://dev-to-uploads.s3.amazonaws.com/i/7l7znwd69ctzp9511s1j.jpg)

Now it's `display: 'block'` which should put the error on it's own line.

![45-message-error-display-block-rendered](https://dev-to-uploads.s3.amazonaws.com/i/xc4y2ebmi9ds2bcd0smr.jpg)

It would also be nice if we could tell the user a field is required before they hit the submit button. We'll do that by adding `mode: 'onBlur'` and pass that into `validation`.

![46-form-validation-mode-onBlur](https://dev-to-uploads.s3.amazonaws.com/i/wpdlpvig8uzyhs09v7hq.jpg)

Now when we enter a field and leave without filling it out we are immediately given feedback.

![47-form-validation-mode-onBlur-rendered](https://dev-to-uploads.s3.amazonaws.com/i/m9i7zrgesaq2sl1exxft.jpg)

And for now that's our entire form. Here's a look at all the form code.

![48-entire-form](https://dev-to-uploads.s3.amazonaws.com/i/23faa5uxpnw0yftygxj6.jpg)

In the [next part](https://dev.to/ajcwebdev/a-first-look-at-redwood-js-part-6-a25) we'll connect our contact form to our database so we can persistent the data entered into the form.


# Part 6 - GraphQL

In [part 5](https://dev.to/ajcwebdev/a-first-look-at-redwood-js-part-5-2ol4) we generated a contact page and took input from the user. In this part we'll connect our contact form to our database so we can persistent the data entered into the form.

To modify our database we'll go to our `schema.prisma` file and add a `Contact` model.

![01-Contact-model](https://dev-to-uploads.s3.amazonaws.com/i/c43cyb5b5fx9okxnjwk3.jpg)

The model takes the `name`, `email`, and `message` strings from the form inputs. It creates an `id` with `autoincrement()` and `createdAt` time with `now()`.

Enter `yarn redwood db save` to create a migration schema.

![02-db-save](https://dev-to-uploads.s3.amazonaws.com/i/xn7b5ogaaiewjuclfb0z.jpg)

You'll be asked to name the migration. I named mine `create-contact`.

![03-name-of-migration](https://dev-to-uploads.s3.amazonaws.com/i/5rsuqs9tccetjg86hfcu.jpg)

This will create another `migrations` directory with a schema file, README, and `steps.json` file like we saw in part 3.

![04-migrate-save--name](https://dev-to-uploads.s3.amazonaws.com/i/qie8znsllijf4yseb0gj.jpg)

Enter `yarn redwood db up` to apply that migration to the database.

![05-db-up](https://dev-to-uploads.s3.amazonaws.com/i/tu2fu0ca9dgwat65am53.jpg)

This will output the database actions applied after the migration.

![06-migrate-up](https://dev-to-uploads.s3.amazonaws.com/i/e1z7owcfkxkwdipidjhw.jpg)

Database actions include three `RawSql` statements and one `CreateTable` statement.

Lastly a Prisma client will be generated.

![07-generate-Prisma-client](https://dev-to-uploads.s3.amazonaws.com/i/yug1wkswfh90w6xdu4rm.jpg)

Enter `yarn redwood generate sdl contact` to create the schema definition language for the contact form.

![08-generate-sdl-contact](https://dev-to-uploads.s3.amazonaws.com/i/qqiyvy9b9cgi7aze3j80.jpg)

This will create an sdl in your `graphql` folder and a resolver in your `services` folder.

![09-generating-SDL-files](https://dev-to-uploads.s3.amazonaws.com/i/v2g3y3y00f8rccgebebr.jpg)

We created three files:
* `contacts.sdl.js` in the `graphql` folder
* `contacts.js` in the `services/contacts` folder
* `contacts.test.js` in the `services/contacts` folder

![10-api-src-folder](https://dev-to-uploads.s3.amazonaws.com/i/jl7rrs5f0p3ox0jyrc9q.jpg)

Lets take a look at our schema definition language first.

![11-contacts.sdl.js](https://dev-to-uploads.s3.amazonaws.com/i/jadii0kc8jhuws7fu4qx.jpg)

The sdl has a `Contact` type and a `Query` type and inputs for creating a contact and updating a contact. Everything that is required for the database is required for GraphQL.

We need to create our own mutation. We don't get this by default because the sdl generator doesn't know what we plan to do with the schema.

![12-type-Mutation](https://dev-to-uploads.s3.amazonaws.com/i/4khk66kfbb87madmzo02.jpg)

Our `Mutation` type will be called `createContact`. The input is `CreateContactInput!` and it returns `Contact`.

Now lets look at our `contacts` service. It has a resolver for the `Query` type from our sdl.

![13-contacts.js](https://dev-to-uploads.s3.amazonaws.com/i/tkmvc85is2u7mrpajrbm.jpg)

Lets create a resolver for `createContact`.

![14-createContact-resolver](https://dev-to-uploads.s3.amazonaws.com/i/ak4zrylmiiviabn4l3ic.jpg)

This takes `input` from the browser and adds it to the database.

In our `ContactPage` file we'll add the mutation and assign it to `CREATE_CONTACT`. It is a common convention to use all caps for our mutations.

![15-CREATE_CONTACT-mutation](https://dev-to-uploads.s3.amazonaws.com/i/dyhfa9i70wo5npmuraax.jpg)

We will just return the `id` since the user will not see this.

Inside the `ContactPage` component we'll call `useMutation()`. We pass an object `create` with variables that are defined in `CREATE_CONTACT`.

![16-useMutation](https://dev-to-uploads.s3.amazonaws.com/i/jqytpgppsleqfwaiytbd.jpg)

The input is the actual object containing the `data` which is assigned to `variables` and passed to the `create()` function inside `onSubmit`.

Make sure to import `useMutation` at the top of the file.

![17-import-useMutation](https://dev-to-uploads.s3.amazonaws.com/i/qy9rbqv38umqyda5b5vj.jpg)

We are now ready to enter our data. Enter a name, email, and message and click the Save button.

![18-form-input](https://dev-to-uploads.s3.amazonaws.com/i/iej5joqzutcnrymnymds.jpg)

Our form gives us the following object which we saw in the previous part.

![19-form-input-console-log](https://dev-to-uploads.s3.amazonaws.com/i/kvcgouy4bnafsxp30cyg.jpg)

We can now check to make sure it was saved. Remember all the way back in part 1 when we said there was something else running on `localhost:8911`?

![20-localhost-8911](https://dev-to-uploads.s3.amazonaws.com/i/dhdqv7dy8r5okpi3dizm.jpg)

This is how we access the graphiQL interface. Click the graphql link.

![21-graphiQL](https://dev-to-uploads.s3.amazonaws.com/i/gocu73heuv7b92vyooyz.jpg)

GraphiQL is like an IDE for your GraphQL queries. On the left side you'll enter a query, and after clicking the middle play button the response will appear on the right side.

Lets create a `contact` query that will return all the `contacts` in the database.

![22-contact-query](https://dev-to-uploads.s3.amazonaws.com/i/skitmwpammuhs1j9rx88.jpg)

We'll ask for the `id`, `name`, `email`, and `message`.

Click the play button and on the right side you'll receive a `data` object containing whatever your entered into your form.

![23-contact-data](https://dev-to-uploads.s3.amazonaws.com/i/efazzobjp57xlnrrg10w.jpg)

The `data` object contains a `contacts` array with objects containing the form input.

There's a few more things we can add to our form to make the user experience a little better. We want to give the user some immediate feedback after they click the save button. We also want to put in safeguards in case the user feels like clicking the save button many times in fast succession.

To do this we'll add a `loading` object after `create`.

![24-loading](https://dev-to-uploads.s3.amazonaws.com/i/v19mts3la6gn4ndwwzon.jpg)

`loading` will be true while the mutation is being performed, and will change to false when the mutation is complete.

We will add `disabled` to the `Submit` button and pass it the `loading` object.

![25-Submit-disabled-loading](https://dev-to-uploads.s3.amazonaws.com/i/ly3s1q3cfrglcu0ujy2f.jpg)

While the mutation is in progress disabled is true, and once it is complete it will change to false.

To test this out go to your Network tab in your browsers devtools. Here we can simulate slow 3G.

![26-slow-3G](https://dev-to-uploads.s3.amazonaws.com/i/s8yz7ik6srnez501wich.jpg)

Enter some more data and click the Save button.

![27-save-button-greyed-out](https://dev-to-uploads.s3.amazonaws.com/i/xhk3hsq685x9vbigl660.jpg)

Now when you click the Save button it will be greyed out for a moment while the input is saved to the database.

Another problem with this form is the input sticks around on the page even after it is submitted. It would be better if we cleared the fields after submitting.

We can do this by importing `useForm` from `react-hook-form`.

![28-import-useForm](https://dev-to-uploads.s3.amazonaws.com/i/qm40kw1ilmxmhmrau32h.jpg)

Inside our `ContactPage` component we'll create a `formMethods` variable and assign it the `useForm()` function that we just imported.

![29-formMethods](https://dev-to-uploads.s3.amazonaws.com/i/g5cpom8hvye3qb433agh.jpg)

Inside `<Form>` we'll add `formMethods` and pass it `formMethods` as a prop.

![30-Form-formMethods](https://dev-to-uploads.s3.amazonaws.com/i/4huv3mrojbtg8ei9515e.jpg)

This gives us access to the reset function. In `useMutation` we'll add a second parameter, which is a callback called `onCompleted`.

![31-onCompleted](https://dev-to-uploads.s3.amazonaws.com/i/7jsntqefz3d350cnckey.jpg)

When the mutation is complete we'll call `formMethods.reset()` and display an `alert()` saying `'Thanks for the message!'`

Lets test this out in our browser. Enter some more data and click the Save button.

![32-alert-thanks-for-the-message](https://dev-to-uploads.s3.amazonaws.com/i/pkh5dc09mtfxdfgcsto4.jpg)

First the alert message appears on the screen. After clicking Ok the form will be cleared.

![33-form-cleared](https://dev-to-uploads.s3.amazonaws.com/i/cde29kj2j1nussmbrxvu.jpg)

Another thing we can improve is the label. Right now it is just defaulting to whatever is entered as the `name` attribute in `<Label>`.

We can add a closing `</Label>` tag and enter something between the tags to change the label. Let's capitalize the labels.

![34-Name-label](https://dev-to-uploads.s3.amazonaws.com/i/f2c1zxdshjp3mafjesf5.jpg)

![35-Email-label](https://dev-to-uploads.s3.amazonaws.com/i/oxqk7l87px13roqlahrw.jpg)

![36-Message-label](https://dev-to-uploads.s3.amazonaws.com/i/nkijmhmo2y1iirldiv2q.jpg)

Check your form for the changes.

![37-updated-form-labels](https://dev-to-uploads.s3.amazonaws.com/i/vot61he4m2gqffmhc5zc.jpg)

Right now we just have client side validation. We also want to validate the input again when it hits the database, so the last thing we'll add is server side validation.

We'll do this in our `contacts.js` file inside the `services/contacts` folder. This is the last place the data travels before entering the database.

First import `UserInputError` from `@redwoodjs/api`.

![38-import-UserInputError](https://dev-to-uploads.s3.amazonaws.com/i/ed684sc1mj3i8qhglbwl.jpg)

Then we'll create a `validate` function that takes the `input` and checks if there is an input for email and if it matches the email regex.

![39-validate-function](https://dev-to-uploads.s3.amazonaws.com/i/5zsq2odq9tnalv4kca6r.jpg)

If there is no input or it isn't a valid email it will throw an object with an error message.

Add this function to `createContact` and pass it the input right before returning the input to the database.

![40-validate-input](https://dev-to-uploads.s3.amazonaws.com/i/shcd9lnx0k4ljz4ayqt8.jpg)

To get access to this we'll go back to our `ContactPage` file and pass `error` into our mutation after the `loading` object.

![41-error-useMutation](https://dev-to-uploads.s3.amazonaws.com/i/2q8ijixqc9cc15pwu8h3.jpg)

Redwood gives us another helper to do this. Import `FormError` at the top of the page.

![42-import-FormError](https://dev-to-uploads.s3.amazonaws.com/i/436i7gv1obqvxelposwh.jpg)

After the opening `<Form>` tag we'll add the `<FormError>` tag. Enter `error={error}` and close off the tag. Finally add `error={error}` to the `<Form>` tag itself.

![43-Form-error-error](https://dev-to-uploads.s3.amazonaws.com/i/8hivftrgxfyv8po89rt9.jpg)

Now we get an error from the server at the top of the page.

![44-cant-create-new-contact](https://dev-to-uploads.s3.amazonaws.com/i/5jgvz9g4h0yzu2524vkg.jpg)

In the [next part](https://dev.to/ajcwebdev/a-first-look-at-redwood-js-part-7-22b0) we'll finally deploy our project to the internet with Netlify and Heroku.

# Part 7 - Deploy

In this [penultimate](https://www.merriam-webster.com/dictionary/penultimate) part we will:
* Deploy our frontend application with Serverless functions on Netlify
* Deploy our backend to a hosted Postgres database on Heroku

First you will need a Github repo with your Redwood project. Mine is [here](https://github.com/ajcwebdev/ajcwebdev/) and contains branches that match up with the state of the project at the end of each of the first six parts. You'll want to make sure the latest branch is merged into the main branch.

![02-github-repo](https://dev-to-uploads.s3.amazonaws.com/i/oqxtndfdnigckcbfe0ge.jpg)

Next you'll need an account on [Netlify](http://netlify.com/).

![03-netlify-sites](https://dev-to-uploads.s3.amazonaws.com/i/gsqffnnk0hljq7i1m91d.jpg)

Click `New site from Git` to create a new site from git.

![04-new-site-from-git](https://dev-to-uploads.s3.amazonaws.com/i/1b8eka5x2xzfij2dguum.jpg)

You can also use GitLab or Bitbucket. 

![05-create-a-new-site](https://dev-to-uploads.s3.amazonaws.com/i/rf47bzvdpckdcrcu89mz.jpg)

Enter the name of your repo into the search bar.

![06-ajcwebdev-repo](https://dev-to-uploads.s3.amazonaws.com/i/7ga9cvn445ujqaizti5d.jpg)

Select the repo.

![07-ajcwebdev/ajcwebdev](https://dev-to-uploads.s3.amazonaws.com/i/4v0psjhaw7ea41cntjie.jpg)

Redwood should select the following build instructions by default.

![08-build-defaults](https://dev-to-uploads.s3.amazonaws.com/i/qrnaw4skocvlwzfee0l8.jpg)

Click `Deploy site` to deploy the site.

![09-site-deploy-in-progress](https://dev-to-uploads.s3.amazonaws.com/i/572nknzho262jp870t9x.jpg)

If we go to the `Deploys` section we can see more information about the build.

![10-netlify-deploys](https://dev-to-uploads.s3.amazonaws.com/i/0ohsanro33avkm5e25n2.jpg)

Your build should take at least a minute or more, so don't freak out if it doesn't work immediately.

![11-deploy-published](https://dev-to-uploads.s3.amazonaws.com/i/gey04r5sox4b2kg3b35u.jpg)

Our deploy took 1 minute and 35 seconds and we can also see a summary of the deploy.

![12-deploy-summary](https://dev-to-uploads.s3.amazonaws.com/i/cvzuzyy424g8x4p2pwak.jpg)

We haven't really deployed the site though, because right now we just have the frontend deployed to Netlify. But we haven't done anything with our database so we should expect an error:

![13-error-502](https://dev-to-uploads.s3.amazonaws.com/i/h3usifvixdlpef3ly033.jpg)

To get our database online we'll need to set up another account and project on [Heroku](heroku.com).

![14-heroku-apps](https://dev-to-uploads.s3.amazonaws.com/i/2q0t1aqwqn6988wpkev2.jpg)

If this is your first project you can click the `Create new app` button in the middle to create a new app or you can click the `New` button on the top right.

![15-create-new-app](https://dev-to-uploads.s3.amazonaws.com/i/vw15vd439zqqtxp5jro6.jpg)

We'll give the app the same name as the Github repo.

![16-app-name-ajcwebdev](https://dev-to-uploads.s3.amazonaws.com/i/rn0nb2tu3e2w6hn5oj9t.jpg)

Now we have a dashboard for our project much like we did in Netlify.

![17-heroku-deploy](https://dev-to-uploads.s3.amazonaws.com/i/kcz8vpv2dubbdjbfe400.jpg)

Lets take a look at our `Resources` tab so we can provision our database.

![18-heroku-resources](https://dev-to-uploads.s3.amazonaws.com/i/bsspznyekikwp5ykb8va.jpg)

Click `Find more add-ons` to find more add-ons.

![19-find-more-add-ons](https://dev-to-uploads.s3.amazonaws.com/i/iiloqno840koo34sh8vl.jpg)

There are many add-ons. We only need one, Heroku Postgres. Why Postgres? [Because Postgres is the best database. There is no other database (02:37)](https://www.heavybit.com/library/podcasts/jamstack-radio/ep-35-graphql-querying-with-hasuras-tanmai-gopal/).

![20-heroku-postgres](https://dev-to-uploads.s3.amazonaws.com/i/opa5syr4igu12lzybb7x.jpg)

Click `Install Heroku Postgres` to install Heroku Postgres.

![21-install-heroku-postgres](https://dev-to-uploads.s3.amazonaws.com/i/iqkc8u5w9ku2l9h0zqyy.jpg)

You can select your add-on plan, we'll be using the free option.

![22-provision-add-on](https://dev-to-uploads.s3.amazonaws.com/i/jtc3jh4e44cbncuw2apu.jpg)

Enter the name of your heroku app and it should appear in the autocomplete.

![23-app-to-provision-to](https://dev-to-uploads.s3.amazonaws.com/i/pnz7t87xknbmd2juxdb5.jpg)

Select your project and click `Provision add-on` to provision the add-on.

![24-click-provision-add-on-button](https://dev-to-uploads.s3.amazonaws.com/i/trg087x8p3ap259mkpf1.jpg)

Now our database is installed.

![25-app-provisioned](https://dev-to-uploads.s3.amazonaws.com/i/vq4q9dk3kddee29vii8m.jpg)

Lets go to the `Settings` tab so we can connect this database to our frontend. Click `Reveal Config Vars` to reveal the config variables.

![26-heroku-settings](https://dev-to-uploads.s3.amazonaws.com/i/89eall7eshul9v3jpk51.jpg)

We can see a key/value pair for the database URL, normally it wouldn't be wise to share environment variables online, but this project is purely explanatory and won't be holding any sensitive data.

![27-enter-config-vars](https://dev-to-uploads.s3.amazonaws.com/i/h851tvjmkn1k8nuci0h8.jpg)

Select the value and copy it to your clipboard. We'll be using this back in our Netlify project.

![28-copy-postgres-vars](https://dev-to-uploads.s3.amazonaws.com/i/tdbwdkrtuhovjv7j71qr.jpg)

Select `Deploy settings` to go to your deploy settings.

![29-netlify-deploys](https://dev-to-uploads.s3.amazonaws.com/i/l7314ljzh8uf6u5vgt0o.jpg)

Under `Build & deploy` select `Environment`.

![32-environment-variables](https://dev-to-uploads.s3.amazonaws.com/i/oencxni0wlxc7fzjj7pz.jpg)

Click the `Edit variables` button to edit the variables.

![33-edit-variables](https://dev-to-uploads.s3.amazonaws.com/i/q0a0k2bapyqhzq6phdbq.jpg)

We're going to use the key/value pair from our Heroku Postgres app.

![34-set-environment-variables](https://dev-to-uploads.s3.amazonaws.com/i/laxg642p28rty060zpjb.jpg)

First enter `DATABASE_URL` for the key.

![35-DATABASE_URL](https://dev-to-uploads.s3.amazonaws.com/i/4a1q892c8p33dd4384n1.jpg)

Then paste the value.

![36-paste-postgres-vars](https://dev-to-uploads.s3.amazonaws.com/i/6rp62306rnvvhm9m0glw.jpg)

At the end of the value add `?connection_limit=1`. This makes sure that each AWS Lambda only opens one database connection.

![37-add-connection-limit](https://dev-to-uploads.s3.amazonaws.com/i/122c8k9jgxymmjas0wjr.jpg)

We'll create one more variable.

![38-new-variable](https://dev-to-uploads.s3.amazonaws.com/i/dw8kgm76770kozcl3i7n.jpg)

It will be called `BINARY_TARGET` with the value `rhel-openssl-1.0-x`.

![39-BINARY_TARGET](https://dev-to-uploads.s3.amazonaws.com/i/i36b0ueh2ie3rnp2tq2t.jpg)

This is a setting for Prisma which needs to know how to generate the client libraries to access the database. Usually it can auto detect that.

However, in this case the libraries that are being built on Netlify are running on Ubuntu. The API deployed to AWS Lambda is running a flavor of RedHat Enterprise Linux. We need to let Prisma know to build for RedHat and not for Ubuntu ([thanks Rob for the explanation (04:09)](https://www.youtube.com/watch?v=UpD3HyuZkvY)).

![40-save-variables](https://dev-to-uploads.s3.amazonaws.com/i/wk7akue4m5mxm3a1l459.jpg)

If we go back to our code in `schema.prisma` we can see that we set our datasource to the environment variable `DATABASE_URL` and our client to `BINARY_TARGET`.

![41-schema-datasource-generator](https://dev-to-uploads.s3.amazonaws.com/i/nr6dw5tqryjt9mkf03cv.jpg)

And then Prisma looks up our local environment file. We override these once you deploy to Netlify.

![42-env.defaults](https://dev-to-uploads.s3.amazonaws.com/i/96qfggo0xtf1shzcwjun.jpg)

Click the `Trigger deploy` button to trigger a deploy and select `Deploy site` to deploy the site. 

![43-trigger-deploy](https://dev-to-uploads.s3.amazonaws.com/i/zytfidzhpakovjtb3c1p.jpg)

You will now receive a great series of logs.

![44-build-logs-1](https://dev-to-uploads.s3.amazonaws.com/i/z40cboxq13wp1mrp3fn1.jpg)

The logs will detail the build process.

![45-build-logs-2](https://dev-to-uploads.s3.amazonaws.com/i/8yy4l7k14bufb3u4s7ig.jpg)

Do not concern yourself with the logs.

![46-build-logs-3](https://dev-to-uploads.s3.amazonaws.com/i/eootzwb58yjda38pbike.jpg)

Let the logs wash over you and through you.

![47-build-logs-4](https://dev-to-uploads.s3.amazonaws.com/i/prcyns2i2i2kbvmtu5wf.jpg)

Raft is a [bunch of logs that get you off Paxos island](https://www.youtube.com/watch?v=w9GP7MNbaRc&t=31m47s).

![48-build-logs-5](https://dev-to-uploads.s3.amazonaws.com/i/la1l401gkdl7hjmq3h0l.jpg)

Now let's go back to our site.

![49-website-empty](https://dev-to-uploads.s3.amazonaws.com/i/q1l566zivlxxzhm17k4k.jpg)

Lets create a new post.

![50-posts](https://dev-to-uploads.s3.amazonaws.com/i/zyj83rse42utpkes6fdp.jpg)

Click the `NEW POST` button to make a new post. Enter a title and body.

![51-new-post](https://dev-to-uploads.s3.amazonaws.com/i/mvvxj6fakcacjpfxni42.jpg)

Save the new post.

![52-first-post-created](https://dev-to-uploads.s3.amazonaws.com/i/39jf6jl3atvs4bkih0gq.jpg)

Lets try to edit our new post.

![53-first-post-edit](https://dev-to-uploads.s3.amazonaws.com/i/gnrv1fxfx8f75gcg5c4o.jpg)

Save your edit to the post.

![54-first-post-edit-working](https://dev-to-uploads.s3.amazonaws.com/i/gumgl08iaq5b3ndae1rk.jpg)

It looks like it's working. Lets check the front page to make sure it's really working.

![55-front-page-working](https://dev-to-uploads.s3.amazonaws.com/i/ebsgis2sngfwh7qoon6p.jpg)

In the next and final part we'll add authentication to our application, something that has never confused any developer ever.

# Part 8 - Auth

# Reflection

# Podcasts
# Blogging