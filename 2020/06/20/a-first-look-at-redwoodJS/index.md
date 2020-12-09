---
title: A First Look at RedwoodJS
date: "2020-06-20"
description: Redwood is an opinionated, full-stack, serverless web application framework for building and deploying JAMstack applications.
---

# Part 1 - Setup

> *I like to think that most things can be achieved. Whatever you have in your head you can probably pull off with code as long as it's possible within the constraints of the universe. It's just a matter of time...and money...and attention.*  
***Tom Preston-Werner - [Full Stack Radio 138](https://www.fullstackradio.com/episodes/138)***

|Introduction|Tutorial|
|------------|--------|
|[I - Redwood Philosophies](https://dev.to/ajcwebdev/redwood-1d46)|Part 1 - Setup|
|[II - Full Stack React](https://dev.to/ajcwebdev/full-stack-react-1ihi)|[Part 2 - Routes](https://dev.to/ajcwebdev/a-first-look-at-redwood-js-part-2-44ph)|
|[III - Jamstack](https://dev.to/ajcwebdev/a-short-history-of-the-jamstack-3lk7)|[Part 3 - Prisma](https://dev.to/ajcwebdev/a-first-look-at-redwood-js-part-3-5ao5)|
|[IV - Serverless](https://ajcwebdev.substack.com/p/42-a-short-history-of-serverless)|[Part 4 - CRUD](https://dev.to/ajcwebdev/a-first-look-at-redwood-js-part-4-2m0g)|
||[Part 5 - Contact](https://dev.to/ajcwebdev/a-first-look-at-redwood-js-part-5-2ol4)|
||[Part 6 - GraphQL](https://dev.to/ajcwebdev/a-first-look-at-redwood-js-part-6-a25)|
||[Part 7 - Deploy](https://dev.to/ajcwebdev/a-first-look-at-redwood-js-part-7-22b0)|
||[Part 8 - Auth](https://dev.to/ajcwebdev/a-first-look-at-redwood-js-part-8-3pjc)|

[Redwood](https://dev.to/ajcwebdev/redwood-1d46) is an opinionated, [full-stack](https://dev.to/ajcwebdev/full-stack-react-1ihi), [serverless](https://dev.to/ajcwebdev/fauna-3mnm) web application framework for building and deploying [JAMstack](https://dev.to/ajcwebdev/a-short-history-of-javascript-4lho) applications.

I've structured this series to reflect the actual process I go through when experimenting with a new framework for the first time. I stick to the path laid out in the official docs tutorial, but as I go through each step I reference the documentation for each command or component. This helps me build a mental model of the framework instead of just copy-pasting commands and code snippets.

I will start at the very beginning and assume no prior knowledge of Redwood although I do assume a basic knowledge of React. But I'm talking really basic, if you know what a component is, have written at least a dozen lines of JSX, and have generated at least one project with [create-react-app](https://reactjs.org/docs/create-a-new-react-app.html) then you'll be fine.

If none of that made sense you should click the link to the create-react-app docs and work through those before reading this. This series is geared towards someone who has at least a few months experience in a coding bootcamp or on the job, around the point where they start getting comfortable with the basic workflows of git, npm, the terminal, and simple HTML websites.

You'll need `yarn` for this tutorial which has slight differences from `npm`. If you've never used `yarn` you can find installation instructions [here](https://yarnpkg.com/getting-started/install) or just enter `yarn install` into your terminal.

# 1.1 `yarn create redwood-app`

The first step is to install Redwood globally to my system and generate our first project. We'll accomplish both of these with the `yarn create` command.

```
yarn create redwood-app ./ajcwebdev
```

This will create a folder called `ajcwebdev` that holds all the code that will be generated. You can call your project anything you want, just make sure to keep using your name anytime I use `ajcwebdev` in a terminal command.

![01-yarn-creating-redwood-app](https://dev-to-uploads.s3.amazonaws.com/i/lxd8utprctvlo5m3qghu.jpg)

# 1.2 `yarn redwood dev`

`yarn rw` is the same as `yarn redwood` and can be used to save a few keystrokes if you want. We'll `cd` into that folder and then start our development server.

```
cd ajcwebdev
yarn rw dev
```

`yarn redwood dev` can be used to run a development server for the Redwood server, Webpack server or your database "server" which isn't exactly a server.

![02-yarn-redwood-dev](https://dev-to-uploads.s3.amazonaws.com/i/dgctwlag1lzlp5t9x006.jpg)

Don't worry about any of that for now but that'll be important in later articles.

Our server is now running on localhost:8910 (a mnemonic to help remember that is thinking of counting 8-9-10). Open a web browser and enter localhost:8910 into the address bar. If you've done everything correctly up to this point you'll see the Redwood starter page.

![03-redwood-starter-page](https://dev-to-uploads.s3.amazonaws.com/i/o2r8f3spa2n3kk7cxv04.jpg)

WHOOPS, it worked, we're up and running.

Don't worry too much about what it says about custom routes, we'll talk about that in the next article. Lets look at the file structure that has been created for us.

![04-project-structure](https://dev-to-uploads.s3.amazonaws.com/i/xvlr8i9s57466ew5h582.jpg)

Don't worry about most of this, for the purpose of this article we'll only be working in the `web` folder. Since we are responsible developers the first thing we do is go to the README.

![05-README](https://dev-to-uploads.s3.amazonaws.com/i/3l125cxaqyia1p7niyg7.jpg)

The README provides instructions for the commands that we used earlier to get our application set up, `yarn install` and `yarn redwood dev`. It also mentions something you may have noticed earlier, we have something else running on `localhost:8911`.

![06-serverless-functions](https://dev-to-uploads.s3.amazonaws.com/i/blxty5qybhlafl59qf39.jpg)

Once again, don't worry if that doesn't make sense since it's outside the scope of this article.

In Redwood our frontend code is contained in the `web` folder and our backend code is contained in the `api` folder. Lets now look at our `web` folder.

![07-project-structure-web](https://dev-to-uploads.s3.amazonaws.com/i/6vqn2so0et6e0sma03gx.jpg)

Redwood structures the `web` folder a bit like create-react-app projects with a `public` and `src` folder.

![08-public-src-directories](https://dev-to-uploads.s3.amazonaws.com/i/t13atdndtlae318ercnu.jpg)

# 1.3 `redwood generate page`

With our application now set up we can start creating pages. We'll use the `generate page` command to create a home page and a folder to hold that page.

```
yarn rw g page home /
```

This created files for our home page and another file for testing that page.

![09-yarn-redwood-generating-HomePage](https://dev-to-uploads.s3.amazonaws.com/i/hzvo9llg8f37bjbji18x.jpg)

Since I only entered `home` it will use that to name both the folder and the component file but you can specify each if necessary.

![10-project-structure-web-src-pages](https://dev-to-uploads.s3.amazonaws.com/i/t1624rsar2mklwuvr4el.jpg)

Return to your browser and you will now see a new page instead of the landing page.

![11-HomePage](https://dev-to-uploads.s3.amazonaws.com/i/t17uzic0cqdvnccuc9ws.jpg)

Let's look at the code that was generated for this page. It's a component called `HomePage` that returns a `<div>` with a header `<h1>` and a paragraph tag `<p>`.

![12-HomePage-component](https://dev-to-uploads.s3.amazonaws.com/i/hprdsiaqol1834ui38i8.jpg)

This should be pretty self-explanatory if you have experience with React. If this doesn't look familiar it would be helpful to spend a little time studying React by itself before jumping into Redwood.

Now we'll edit the page and see what happens.

![13-HomePage-edit](https://dev-to-uploads.s3.amazonaws.com/i/xwkypgowpocigb25x83o.jpg)

Feel free to include links to your own social accounts. With those changes made return to your browser.

![14-HomePage-new](https://dev-to-uploads.s3.amazonaws.com/i/an4t8t1uk84208zszmh0.jpg)

Now we are going to generate our `about` page.

```
yarn rw g page about
```

Like before we created an `AboutPage` component inside of an `AboutPage` folder along with a file for testing that page.

![15-yarn-redwood-generating-AboutPage](https://dev-to-uploads.s3.amazonaws.com/i/jdlvagogp4v0w0sxqw6z.jpg)

We don't yet have a link to get to it from the home page, so for now you'll need to enter the route manually into your browser address bar by adding `/about` after `localhost:8910`.

![16-AboutPage](https://dev-to-uploads.s3.amazonaws.com/i/1xpgo6slth77gh2kx69g.jpg)

Open up the code and it's another React component much like the last! Components are kind of a big deal in React.

![17-AboutPage-component](https://dev-to-uploads.s3.amazonaws.com/i/16huzchu75d19onjqu5c.jpg)

We can also edit this page just like the `home` page.

![18-AboutPage-edit](https://dev-to-uploads.s3.amazonaws.com/i/74gtu85dnjnrsjyg9hbv.jpg)

With those changes return to your browser.

![19-AboutPage-new](https://dev-to-uploads.s3.amazonaws.com/i/0jb47h2b9nh6ufmgeipn.jpg)

We can also see these files have been added to our `src` folder.

![20-project-structure-web-new](https://dev-to-uploads.s3.amazonaws.com/i/sui0vqkfd50f5oqini8u.jpg)

In the [next part](https://dev.to/ajcwebdev/a-first-look-at-redwood-js-part-2-44ph) we'll take a look at Redwood's router and create links for the pages we created.

# Part 2 - Routes

> *We basically wrote the tutorial the way that we wanted the code to work and then we made the tutorial work by writing the code. As opposed to [Readme Driven Development](https://tom.preston-werner.com/2010/08/23/readme-driven-development.html) which I've written about this is tutorial driven development.*  
> ***Tom Preston-Werner - [Full Stack Radio 138](https://www.fullstackradio.com/episodes/138)***

|Introduction|Tutorial|
|------------|--------|
|[I - Redwood Philosophies](https://dev.to/ajcwebdev/redwood-1d46)|[Part 1 - Setup](https://dev.to/ajcwebdev/a-first-look-at-redwood-js-1017)|
|[II - Full Stack React](https://dev.to/ajcwebdev/full-stack-react-1ihi)|Part 2 - Routes|
|[III - Jamstack](https://dev.to/ajcwebdev/a-short-history-of-the-jamstack-3lk7)|[Part 3 - Prisma](https://dev.to/ajcwebdev/a-first-look-at-redwood-js-part-3-5ao5)|
|[IV - Serverless](https://ajcwebdev.substack.com/p/42-a-short-history-of-serverless)|[Part 4 - CRUD](https://dev.to/ajcwebdev/a-first-look-at-redwood-js-part-4-2m0g)|
||[Part 5 - Contact](https://dev.to/ajcwebdev/a-first-look-at-redwood-js-part-5-2ol4)|
||[Part 6 - GraphQL](https://dev.to/ajcwebdev/a-first-look-at-redwood-js-part-6-a25)|
||[Part 7 - Deploy](https://dev.to/ajcwebdev/a-first-look-at-redwood-js-part-7-22b0)|
||[Part 8 - Auth](https://dev.to/ajcwebdev/a-first-look-at-redwood-js-part-8-3pjc)|

In [part 1](https://dev.to/ajcwebdev/a-first-look-at-redwood-js-1017) we installed and created our first RedwoodJS application. We used:
* `yarn create redwood-app` to generate the initial app
* `redwood generate page` to create:
  * A `HomePage` folder containing a `HomePage` file containing a `HomePage` component
  * An `AboutPage` folder containing an `AboutPage` file containing an `AboutPage` component.

**Quick tip**: If at any point you're having trouble remembering commands just enter:

```
yarn rw --help
```

You'll get a quick reminder of all the commands.

![01-redwood-help](https://dev-to-uploads.s3.amazonaws.com/i/7k2w22h54b19dtdaehvp.jpg)

We were able to navigate between the different pages in our browser by entering `/about` for the about page or a slash (`/`) for the home page. Depending on your experience with React this may have been surprising to you.

If you've worked on routing in React before you know that to achieve this there needs to be an entirely different package imported containing the router and then your routes need to be wrapped in a `<BrowserRouter>` or `<Router>` component to give the router access to your pages. Well guess what.....

# 2.1 `Routes.js`

![02-web-src-routes](https://dev-to-uploads.s3.amazonaws.com/i/6754hyawsc4nhbedcokc.jpg)

In our `src` folder we have a file called `Routes.js`. When we used the CLI to generate `HomePage` and `AboutPage` we also created these routes.

* All Page components from 'src/pages` are auto-imported
* Nested directories are supported, and should be uppercase
* Each subdirectory will be prepended onto the component name

Examples:

`src/pages/HomePage/HomePage.js`         -> `HomePage`
`src/pages/Admin/BooksPage/BooksPage.js` -> `AdminBooksPage`

# 2.2 `index.js`

The other file in our `src` folder is `index.js` which is our root component that ReactDOM renders to the screen.

![03-web-src-index](https://dev-to-uploads.s3.amazonaws.com/i/n4wv8nl5o8p0g78pw5y9.jpg)

In React all [components are composable](https://reactjs.org/blog/2013/06/05/why-react.html) which encourages the creation of reusable UI components that present data that changes over time. Traditionally, web application UIs were built using templates or HTML directives.

But in React you always have a root component that contains other components and those components may contain other components. If that's a little confusing just give it some time and it'll start to click as this series goes on.

The important take away is:

1. Your routes and thus all the website's pages are contained within the `<RedwoodProvider>` tags (we'll talk about these more once we get to state management).
2. The provider itself is contained within the `<FatalErrorBoundary>` component that is taking in `<FatalErrorPage>` as a prop which defaults your website to an error page if all else fails.

# 2.3 `Link`

When it comes to routing, matching URLs to Pages is only half the equation. The other half is generating links to your pages. Lets add a link to our page so we can navigate between our home page and about page by clicking on the page. We'll need to add 3 things to our `HomePage` file:

1. Import `Link` and `routes` from `@redwoodjs/router`
2. `<Link to={}>About</Link>`
3. Pass into the Link component `routes.about()`

![04-HomePage-link-to-about-page](https://dev-to-uploads.s3.amazonaws.com/i/68bt581387fmy95u10wx.jpg)

You use a `Link` to generate a link to one of your routes. The `routes` object can access URL generators for any of your routes.

We call the functions on the `routes` object ***named route functions***. They are named after whatever you specify in the `name` prop of the `Route`.

Return to your browser to see the changes to your home page.

![05-home-page-with-about-link](https://dev-to-uploads.s3.amazonaws.com/i/3yhf1exg9aiyyqn2mpvt.jpg)

We now have a link we can click to navigate to our about page from our home page. Click the link and you will be brought to your about page.

![06-about-page](https://dev-to-uploads.s3.amazonaws.com/i/myah900v6eecz6agqcgn.jpg)

We also want to be able to navigate back to our home page once we are on our about page. We'll do the same three steps from earlier but with a different prop:

1. Import `Link` and `routes` from `@redwoodjs/router`
2. `<Link to={}>About</Link>`
3. Pass into the Link component `routes.home()`

![07-AboutPage-component](https://dev-to-uploads.s3.amazonaws.com/i/eh6oa070pmpwkt8oyl6n.jpg)

Everything is exactly the same except we pass in `routes.home()` instead of `routes.about()` because we want to navigate to our home page this time. Take a look at your about page.

![08-about-page-with-return-home-link](https://dev-to-uploads.s3.amazonaws.com/i/jxmx68c2mwply6jok8m1.jpg)

There is now a link that will take you back to the home page when clicked. If we open up our editor and look at our working tree we can see the changes we added.

![09-HomePage-working-tree](https://dev-to-uploads.s3.amazonaws.com/i/tdzhcl0quo7y4fihhr99.jpg)

You can only see this if you're working with git and regularly committing and pushing your code which is highly recommended.

# 2.4 `redwood generate layout`

You've probably been on a website before. Usually there's some kind of navigation bar at the top and footer at the bottom that stays consistent as you travel around the website.

Redwood's folder structure is designed to make this really easy.

![10-layouts](https://dev-to-uploads.s3.amazonaws.com/i/fhw492184t7gqkysiuci.jpg)

Remember what I said before about everything being a component containing other components? That's the middle part. Pages contain components. Your layout will contain all of your pages.

We can generate a file for our layout with `yarn redwood generate layout` or `yarn rw g layout`. This will work a lot like the `generate page` commands we've done earlier.

```
yarn rw g layout blog
```

The only difference is it will create a folder inside `./web/src/layouts` this time instead of `./web/src/pages` because we are generating a layout and not a page.

![11-generating-BlogLayout](https://dev-to-uploads.s3.amazonaws.com/i/k52wh8jgfhbi01ltvjz3.jpg)

That makes sense. Take a look at your layouts folder and you'll see a file called `BlogLayout.js` and another called `BlogLayout.test.js` for testing.

![12-BlogLayout-folder](https://dev-to-uploads.s3.amazonaws.com/i/ksa3fcmkmau4ts0ahs1n.jpg)

# 2.5 `BlogLayout`

Lets look at our `BlogLayout` component

![13-layout-BlogLayout](https://dev-to-uploads.s3.amazonaws.com/i/h17idf96oqi2ssfjalgd.jpg)

`children` is where the magic will happen. Any page content given to the layout will be rendered here.

![14-BlogLayout-component](https://dev-to-uploads.s3.amazonaws.com/i/3jnvodfeel3xcod1levn.jpg)

Back to HomePage and AboutPage, we add a <BlogLayout> wrapper and now they're back to focusing on the content they care about

![15-HomePage-import-BlogLayout](https://dev-to-uploads.s3.amazonaws.com/i/8u258ya82phsnkb83087.jpg)

We can remove the import for Link and routes from HomePage since those are in the Layout instead:

![16-AboutPage-import-BlogLayout](https://dev-to-uploads.s3.amazonaws.com/i/sidrxk8wibgkixvltw7w.jpg)

Notice that the import statement uses `src/layouts/BlogLayout` and not `../src/layouts/BlogLayout` or `./src/layouts/BlogLayout`.
* This is a convenience feature so you don't need to worry about the nesting of your folders.
* `src` is an alias to the `src` path in the current workspace. If you're working in web then `src` points to `web/src` and in `api` it points to `api/src`.

If we look at our home pages now it should look and behave the same way as before except we have turned our title in the `<h1>` tag into a home page link.

![17-home-page-with-BlogLayout](https://dev-to-uploads.s3.amazonaws.com/i/acyh7mrt05eg63n3g40f.jpg)

Our about page is the same except we have removed the link to return home since we can now click the title.

![18-about-page-with-BlogLayout](https://dev-to-uploads.s3.amazonaws.com/i/v5cpyykmpar9yoc1qikq.jpg)

In the [next part](https://dev.to/ajcwebdev/a-first-look-at-redwood-js-part-3-5ao5) we'll start working with a database and learn to create, retrieve, update, and destroy blog posts.

# Part 3 - Prisma

> *What I wanted was to codify and standardize the types of things that we were already doing and just remove choice and remove friction and just give people the ability to sit down and say, "all right I know these technologies already, I have the prerequisite knowledge to do this."*  
> ***Tom Preston-Werner - [Full Stack Radio 138](https://www.fullstackradio.com/episodes/138)***

|Introduction|Tutorial|
|------------|--------|
|[I - Redwood Philosophies](https://dev.to/ajcwebdev/redwood-1d46)|[Part 1 - Setup](https://dev.to/ajcwebdev/a-first-look-at-redwood-js-1017)|
|[II - Full Stack React](https://dev.to/ajcwebdev/full-stack-react-1ihi)|[Part 2 - Routes](https://dev.to/ajcwebdev/a-first-look-at-redwood-js-part-2-44ph)|
|[III - Jamstack](https://dev.to/ajcwebdev/a-short-history-of-the-jamstack-3lk7)|Part 3 - Prisma|
|[IV - Serverless](https://ajcwebdev.substack.com/p/42-a-short-history-of-serverless)|[Part 4 - CRUD](https://dev.to/ajcwebdev/a-first-look-at-redwood-js-part-4-2m0g)|
||[Part 5 - Contact](https://dev.to/ajcwebdev/a-first-look-at-redwood-js-part-5-2ol4)|
||[Part 6 - GraphQL](https://dev.to/ajcwebdev/a-first-look-at-redwood-js-part-6-a25)|
||[Part 7 - Deploy](https://dev.to/ajcwebdev/a-first-look-at-redwood-js-part-7-22b0)|
||[Part 8 - Auth](https://dev.to/ajcwebdev/a-first-look-at-redwood-js-part-8-3pjc)|

In [part 1](https://dev.to/ajcwebdev/a-first-look-at-redwood-js-1017) we installed and created our first RedwoodJS application and in [part 2](https://dev.to/ajcwebdev/a-first-look-at-redwood-js-part-2-44ph) we created links to our different page routes and a reusable layout for our site.

In this part we'll get our database up and running and learn to create, retrieve, update, and destroy blog posts.

So far we've been working in the `web` folder. In our `api` folder there is a folder called `prisma` for our Prisma schema.

![01-project-structure-api](https://dev-to-uploads.s3.amazonaws.com/i/hct10louzlva7xdmtk1l.jpg)

Prisma is a [query builder](https://www.prisma.io/docs/understand-prisma/why-prisma) that provides a type-safe API for submitting database queries which return JavaScript objects.

It is similar to an ORM and was selected by Tom in the hopes of emulating [Active Record's](https://guides.rubyonrails.org/active_record_basics.html) role in Ruby on Rails.

![02-prisma-folder](https://dev-to-uploads.s3.amazonaws.com/i/4dqvsgehyumpz7mtqffd.jpg)

# 3.1 `schema.prisma`

The Prisma schema file is the main configuration file for your Prisma setup. It is typically called `schema.prisma`

![03-schema-prisma](https://dev-to-uploads.s3.amazonaws.com/i/begc53wcy4jwy9hdtku5.jpg)

In order to set up Prisma Client, you need a Prisma schema file with:
* your database connection
* the Prisma Client `generator`
* at least one `model`

We'll delete the default `UserExample` model and make a `Post` model with an `id`, `title`, `body`, and `createdAt` time.

![04-schema-prisma-Post-model](https://dev-to-uploads.s3.amazonaws.com/i/5spibfw09dz3gabmb2uy.jpg)

# 3.2 `seeds.js`

`seeds.js` is used to populate your database with any data that needs to exist for your app to run at all (maybe an admin user or site configuration).

![05-seeds](https://dev-to-uploads.s3.amazonaws.com/i/y9b86h5xm8tlhc3uztmf.jpg)

# 3.3 `redwood db save`

Running `yarn rw db save` generates the folders and files necessary to create a new migration.

```
yarn rw db save
```

This will create our database migration.

![06-creating-database-migration](https://dev-to-uploads.s3.amazonaws.com/i/kns0ie08g1wxgvw68wys.jpg)

It is named `migration` by default.

![07-new-datamodel](https://dev-to-uploads.s3.amazonaws.com/i/yrp3vadsltwr9i4ri6rd.jpg)

* **Data sources** specify the details of the data sources Prisma should connect to such as a PostgreSQL database
* **Generators** specify what clients should be generated such as the Prisma Client
* **Data model definition** specifies your application models and their relations

# 3.4 `migrations`

A migration defines the steps necessary to update your current schema.

![08-created-your-migration](https://dev-to-uploads.s3.amazonaws.com/i/susq1wpxa9371jkgpkkr.jpg)

The `migrate` command creates and manages database migrations. It can be used to create, apply, and rollback database schema updates in a controlled manner.

![09-api-folder-structure](https://dev-to-uploads.s3.amazonaws.com/i/hvwoo99bat2dkuye5fc4.jpg)

The `README` contains a human-readable description of the migration.

![10-database-migration-initialize-database](https://dev-to-uploads.s3.amazonaws.com/i/talhgpjwjqmngiv0xg0f.jpg)

It includes metadata like:
* when the migration was created and by who
* a list of the actual migration changes
* a diff of the changes that are made to the `schema.prisma` file

![11-database-changes](https://dev-to-uploads.s3.amazonaws.com/i/90eygy8pvs57i720hxsj.jpg)

`schema.prisma` in the migration folder is the schema that will be created if the migration is applied to the project.

# 3.5 `steps.json`

`steps.json` is an alternative representation of the migration steps that will be applied.

![12-steps-json](https://dev-to-uploads.s3.amazonaws.com/i/9lc0xu2vgb9tq6rkiqnv.jpg)

Steps are actions that resolve into zero or more database commands. Steps generically describe models, fields and relationships, so they can be easily translated to datasource-specific migration commands.

# 3.6 `redwood db up`

This command generates the Prisma client and applies migrations. The database is migrated up to a specific state.

```
yarn rw db up
```

This will run the commands against the database to create the changes we need. This results in a new table called `Post` with the fields we defined.

![13-migrate-database-up-started](https://dev-to-uploads.s3.amazonaws.com/i/cic7sdqzmmj8gr0bza46.jpg)

The following `datasource` defines a SQLite database.

![14-datamodel-that-will-initialize-the-db](https://dev-to-uploads.s3.amazonaws.com/i/41bddbn17w3erd7edrsu.jpg)

After checking for data loss the database actions will be executed. In this instance we just have a single `CreateTable` statement for our Post model.

![15-database-migration](https://dev-to-uploads.s3.amazonaws.com/i/gptm3u9nng2ifvmreg59.jpg)

The Prisma client will then be generated.

![16-generating-prisma-client](https://dev-to-uploads.s3.amazonaws.com/i/927wf7o2rs6nn3yhc7ys.jpg)

# 3.7 `redwood generate scaffold`

A scaffold quickly creates a CRUD interface for a model by generating all the necessary files and corresponding routes.

```
yarn rw g scaffold post
```

This will generate pages, SDL's, services, layouts, cells, and components based on a given database schema Model. Look at all the stuff I'm not doing!

![17-generating-scaffold-files](https://dev-to-uploads.s3.amazonaws.com/i/bbjsp27lv4jhaap2xizc.jpg)

Open the browser and enter `localhost:8910/posts`.

![18-posts-page](https://dev-to-uploads.s3.amazonaws.com/i/lhz94ndsl9olzxe9fa43.jpg)

We have a new page called Posts with a button to create a new post. If we click the new post button we are given an input form with fields for title and body.

![19-new-post-form](https://dev-to-uploads.s3.amazonaws.com/i/wzd7fuj7095skqrvcjc8.jpg)

We were taken to a new route, `/posts/new`. Let's create a blog post about everyone's favorite dinosaur.

![20-new-deno-post](https://dev-to-uploads.s3.amazonaws.com/i/4232p8zg5u8p3lhrumlc.jpg)

If we click the save button we are brought back to the posts page.

![21-deno-post-created](https://dev-to-uploads.s3.amazonaws.com/i/txd7ni7eggb7pmw1tdtm.jpg)

We now have a table with our first post.

![22-deno-post-edit](https://dev-to-uploads.s3.amazonaws.com/i/hw56jz0iedg3lzmwfzh6.jpg)

When we click the edit button we are taken to a route for the individual post that we want to edit. Each post has a unique id.

![23-deno-post-edited](https://dev-to-uploads.s3.amazonaws.com/i/ba7hs3vyci8bus9w9t6o.jpg)

The title has now been changed from `01-deno` to `01-deno-edit`. Now we'll create another post.

![24-will-delete-post](https://dev-to-uploads.s3.amazonaws.com/i/n6n86mvxjeyjgmj2kxzx.jpg)

If we click the delete button we will be given a warning.

![25-delete-post-warning](https://dev-to-uploads.s3.amazonaws.com/i/8129rzy897ydxzo9s4wi.jpg)

Click ok to confirm and you'll receive a message saying your post has been deleted.

![26-post-deleted](https://dev-to-uploads.s3.amazonaws.com/i/81z536fmmkfdtz241ijd.jpg)

Lets add another blog post:

![27-fauna-post](https://dev-to-uploads.s3.amazonaws.com/i/lt8ao1j6n93ntb0jlevm.jpg)

And one more:

![28-next-post](https://dev-to-uploads.s3.amazonaws.com/i/b22d01flnjys1nh355zs.jpg)

If we make more posts they will start on the id after the deleted item. We already had an id 2. You can't call something else id 2, that would make your database a liar.

![29-all-posts](https://dev-to-uploads.s3.amazonaws.com/i/5z5ecpynu0qhkm4jo62y.jpg)

In the [next part](https://dev.to/ajcwebdev/a-first-look-at-redwood-js-part-4-2m0g) we'll look at the code that powers this functionality and learn about [Cells](https://redwoodjs.com/tutorial/cells). We'll also set up our frontend to query data from our backend to render a list of our blog posts to the front page.

# Part 4 - CRUD

>*What I’ve experienced and what I know many people have experienced learning React and getting into this is that path right now is very, very, very, very, very long. And hard. And horrible.*  
>***Tom Preston-Werner - [Full Stack Radio 138](https://www.fullstackradio.com/episodes/138)***

|Introduction|Tutorial|
|------------|--------|
|[I - Redwood Philosophies](https://dev.to/ajcwebdev/redwood-1d46)|[Part 1 - Setup](https://dev.to/ajcwebdev/a-first-look-at-redwood-js-1017)|
|[II - Full Stack React](https://dev.to/ajcwebdev/full-stack-react-1ihi)|[Part 2 - Routes](https://dev.to/ajcwebdev/a-first-look-at-redwood-js-part-2-44ph)|
|[III - Jamstack](https://dev.to/ajcwebdev/a-short-history-of-the-jamstack-3lk7)|[Part 3 - Prisma](https://dev.to/ajcwebdev/a-first-look-at-redwood-js-part-3-5ao5)|
|[IV - Serverless](https://ajcwebdev.substack.com/p/42-a-short-history-of-serverless)|Part 4 - CRUD|
||[Part 5 - Contact](https://dev.to/ajcwebdev/a-first-look-at-redwood-js-part-5-2ol4)|
||[Part 6 - GraphQL](https://dev.to/ajcwebdev/a-first-look-at-redwood-js-part-6-a25)|
||[Part 7 - Deploy](https://dev.to/ajcwebdev/a-first-look-at-redwood-js-part-7-22b0)|
||[Part 8 - Auth](https://dev.to/ajcwebdev/a-first-look-at-redwood-js-part-8-3pjc)|

In [part 1](https://dev.to/ajcwebdev/a-first-look-at-redwood-js-1017) we installed and created our first RedwoodJS application, in [part 2](https://dev.to/ajcwebdev/a-first-look-at-redwood-js-part-2-44ph) we created links to our different page routes and a reusable layout for our site, and in [part 3](https://dev.to/ajcwebdev/a-first-look-at-redwood-js-part-3-5ao5) we got our database up and running and learned to create, retrieve, update, and destroy blog posts.

In this part we'll look at all the code that was generated that allowed us to perform our CRUD operations on the blog posts. We'll also set up our frontend to query data from our backend to render a list of our blog posts to the front page. If you've never worked with [GraphQL](https://www.howtographql.com/) or serverless functions like [Lambda](https://www.serverless.com/aws-lambda/) then some of the concepts in this part may be new.

If you want to learn more I have a post about [the history of GraphQL, current projects, and resources](https://dev.to/ajcwebdev/a-short-history-of-graphql-20nb).

# 4.1 `api/src`

We've seen the `prisma` folder under `api`, now we'll look at the `src` folder containing our GraphQL code. Redwood comes with GraphQL integration built in to make it easy to get our client talking to our serverless functions.

![01-api-src-folder](https://dev-to-uploads.s3.amazonaws.com/i/p4fn5syh1i8ruaknq2mx.jpg)

# 4.2 `graphql.js`

The `functions` folder will contain any lambda functions your app needs in addition to the `graphql.js` file auto-generated by Redwood. This file is required to use the GraphQL API.

![03-api-src-functions-graphql](https://dev-to-uploads.s3.amazonaws.com/i/vv2tq8i55o013gk6ojqn.jpg)

We will be working more with the schema definition language and our services so you don't need to worry too much about what's going on in this file.

I still have no idea what the heck this thing is doing, all I know is it's doing some [Apollo stuff](https://www.apollographql.com/docs/apollo-server/). See [these docs](https://www.npmjs.com/package/@redwoodjs/api) for further explanation.

# 4.3 `posts.sdl.js`

`graphql` contains your GraphQL schema. The files will end in `.sdl.js`. GraphQL schemas for a service are specified using the GraphQL SDL ([schema definition language](https://graphql.org/learn/schema/)) which defines the API interface for the client.

Our `schema` has five object types each with their own fields and types.

![05-api-src-graphql-posts-sdl
](https://dev-to-uploads.s3.amazonaws.com/i/5o4we1jhx17lh4j8efmz.jpg)

### `Post` - A blog post

![06-api-src-graphql-posts-sdl-Post](https://dev-to-uploads.s3.amazonaws.com/i/4kay4muxjejve35nib3u.jpg)

### `Query` - A query that retrieves either:
* multiple posts in an array (line 12)
* a single post with an `id` (line 13)

![07-api-src-graphql-posts-sdl-Query](https://dev-to-uploads.s3.amazonaws.com/i/1zvdg4j316xsj25etds9.jpg)

### `CreatePostInput` - `title` and `body` input of new post

![08-api-src-graphql-posts-sdl-CreatePostInput](https://dev-to-uploads.s3.amazonaws.com/i/qc5tl58xc297sii3m5xf.jpg)

### `UpdatePostInput` - `title` and `body` input of updated post

![09-api-src-graphql-posts-sdl-UpdatePostInput](https://dev-to-uploads.s3.amazonaws.com/i/7fvwnfwnk7ertm6hnwtb.jpg)

### `Mutation` - Create, update, or delete post

![10-api-src-graphql-posts-sdl-Mutation](https://dev-to-uploads.s3.amazonaws.com/i/ptzrabxzayuj3xvfledx.jpg)

`createPost`
* Takes `title` and `body` from `CreatePostInput`
* Creates a `Post`

`updatePost`
* Takes `title` and `body` from `UpdatePostInput`
* Takes `id` of the updated `Post`

`deletePost`
* Takes `id` of the deleted `Post`

# 4.4 `db.js`

`lib` contains one file, `db.js`, which instantiates the Prisma database client. You can use this folder for other code related to the API side that doesn't fit in functions or services.

[Prisma Client](https://www.prisma.io/docs/reference/tools-and-interfaces/prisma-client) is an auto-generated and type-safe query builder that's tailored to your data.

![12-api-src-lib-db](https://dev-to-uploads.s3.amazonaws.com/i/ay5ibk7uzeh0rz85pc8a.jpg)

# 4.5 `posts.js`

`services` contain business logic related to your data. A service implements the logic of talking to the third-party API.

This is where your code for querying or mutating data with GraphQL ends up. The difference is it's in a format that's reusable in other places in your application.

![14-api-src-services-posts](https://dev-to-uploads.s3.amazonaws.com/i/5875tb982w1poimunt5t.jpg)

Redwood will automatically import and map resolvers from the `services` file onto your SDL. You write resolvers in a way that makes them easy to call as regular functions from other [resolvers](https://graphql.org/learn/execution/) or `services`.

Redwood will look in `api/src/services/posts/posts.js` for the following five resolvers:

## `posts`
![14-1-api-src-services-posts-posts](https://dev-to-uploads.s3.amazonaws.com/i/d9us71jk32gdm3607r28.jpg)

## `post`
![14-2-api-src-services-posts-post](https://dev-to-uploads.s3.amazonaws.com/i/5itfxp1tf66h8ylll6az.jpg)

## `createPost`
![14-3-api-src-services-posts-createPost](https://dev-to-uploads.s3.amazonaws.com/i/tr0hh0rift9muttjo8cp.jpg)

## `updatePost`
![14-4-api-src-services-posts-updatePost](https://dev-to-uploads.s3.amazonaws.com/i/zj83x56uh09253wf2izk.jpg)

## `deletePost`
![14-5-api-src-services-posts-deletePost](https://dev-to-uploads.s3.amazonaws.com/i/gjalgcswunobtewv317d.jpg)

# 4.6 `PostPage`

`PostPage` is a component that takes in `PostCell` with a post's `id` as a prop. `PostCell` is wrapped in the `PostsLayout` component.

![15-web-src-pages-PostPage](https://dev-to-uploads.s3.amazonaws.com/i/28pioylp3oqk6no3s42c.jpg)

Here's the view of `PostPage` with a `PostCell` wrapped in the `PostsLayout`:

![16-PostPage-rendered](https://dev-to-uploads.s3.amazonaws.com/i/ytvwsrqml2t7t6nqp6eo.jpg)

# 4.7 `PostsLayout`

![17-layouts-PostsLayout](https://dev-to-uploads.s3.amazonaws.com/i/xumxuzi89chjjrb9tbvn.jpg)

If you click Posts you will be linked to `routes.posts()` and if you click New Post you will be linked to `routes.NewPost()` 

Here's the view of just the `PostsLayout`:

![18-PostsLayout-rendered](https://dev-to-uploads.s3.amazonaws.com/i/h4kubdnasvfwtxce4p38.jpg)

# 4.8 `PostCell`

Cells provide a simpler and more declarative approach to data fetching. When you create a cell you export several specially named constants and then Redwood takes it from there.

Cells should be used when your component needs some data from the database or other service that is delayed in responding. Redwood juggles what is displayed and when.

![19-web-src-components-PostCell](https://dev-to-uploads.s3.amazonaws.com/i/zhdb77u4h5qzkpy4ghbv.jpg)

The minimum you need for a cell are the `QUERY` and `Success` exports.
* If you don't export an `Empty` component, empty results will be sent to your `Success` component.
* If you don't provide a `Failure` component you'll get error output sent to the console.

# 4.9 `Post`

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

# 4.10 `NewPostPage`

`NewPostPage` is a component that takes in `NewPost` wrapped in the `PostsLayout` component. The same `PostsLayout` from `PostPage` is being reused here but with a different component nested inside.

![30-web-src-pages-NewPostPage](https://dev-to-uploads.s3.amazonaws.com/i/3d4iwj8nylkk0hgb5ckb.jpg)

Here's the view:

![31-NewPostPage-rendered](https://dev-to-uploads.s3.amazonaws.com/i/gn3ld4u3r3aeyutjvryx.jpg)

# 4.11 `NewPost`

`NewPost` is a component that takes in data from the `PostForm` component and uses `CREATE_POST_MUTATION` to save the post to the database.

![32-web-src-components-NewPost](https://dev-to-uploads.s3.amazonaws.com/i/e8r7kn63op9wuvic3ewv.jpg)

Here's the view:

![33-new-post-form-rendered](https://dev-to-uploads.s3.amazonaws.com/i/l7mqsdjpj68lqaqtkqua.jpg)

# 4.12 `PostForm`

Redwood provides several helpers to make your life easier when working with forms. It is a wrapper around [react-hook-form](https://react-hook-form.com/).

![34-src-components-PostForm](https://dev-to-uploads.s3.amazonaws.com/i/63mf8q41ms8zmvmkdpg6.jpg)

## `onSubmit`

A prop that accepts a function name or anonymous function to be called if validation is successful. Behind the scenes the handler given to `onSubmit` is given to react-hook-form's [`handleSubmit`](https://react-hook-form.com/api/#handleSubmit) function.

![35-src-components-PostForm-onSubmit](https://dev-to-uploads.s3.amazonaws.com/i/pxb2jzewpip02t3892zg.jpg)

## `<Form>`

Surrounds all form elements and provides contexts for errors and form submission.

![36-src-components-PostForm](https://dev-to-uploads.s3.amazonaws.com/i/u9p64kiu714rywymuxfk.jpg)

## `<FormError>`

Displays an error message, typically at the top of your form, containing error messages from the server

![37-src-components-PostForm-FormError](https://dev-to-uploads.s3.amazonaws.com/i/kopxz4rajuith88cvq7w.jpg)

## `<Label>`

Used in place of the HTML `<label>` tag and can respond to errors with different styling

![38-src-components-PostForm-Title-Label](https://dev-to-uploads.s3.amazonaws.com/i/q2owaav8w3vdqup8pq4o.jpg)

## `<TextField>`

Renders an HTML <input type="text"> field, but is registered with react-hook-form to provide some validation and error handling.

![39-src-components-PostForm-Title-TextField](https://dev-to-uploads.s3.amazonaws.com/i/yyiscrr4pk5zdtwl8ktw.jpg)

## `<FieldError>`

Displays form validation errors and server errors.

![40-src-components-PostForm-Title-FieldError](https://dev-to-uploads.s3.amazonaws.com/i/9vrhbi9fb8p85th2yump.jpg)

Here's the view:

![41-Title-rendered](https://dev-to-uploads.s3.amazonaws.com/i/ei6pkhkp0ftu1nlomkxy.jpg)

`<Label>`, `<TextField>`, and `<FieldError>` are also used for the Body.

![42-Body](https://dev-to-uploads.s3.amazonaws.com/i/rvmxv1baq5toyi7ia4pg.jpg)

Here's the view:

![43-Body-rendered](https://dev-to-uploads.s3.amazonaws.com/i/w3tkymddbblwioxawp4i.jpg)

## `<Submit>`

Used in place of `<button type="submit">` and will trigger a validation check and "submission" of the form. It executes the function given to the `onSubmit` attribute on `<Form>`.

![44-Save](https://dev-to-uploads.s3.amazonaws.com/i/yftnmrnnvh7wu2w6smnx.jpg)

Here's the view:

![45-Save-rendered](https://dev-to-uploads.s3.amazonaws.com/i/vjpc0o4riipmg0yr3pbm.jpg)

And here's the view of the entire `<Form>` component:

![46-PostForm-rendered](https://dev-to-uploads.s3.amazonaws.com/i/3v46mdwsvorcd1gqosim.jpg)

# 4.13 `EditPostPage`

Much like `PostPage`, `EditPostPage` is a component that takes in `EditPostCell` with a post's `id` as a prop. `EditPostCell` is wrapped in the `PostsLayout` component.

![47-web-src-pages-EditPostPage](https://dev-to-uploads.s3.amazonaws.com/i/wv7r7ll0k1vkx970m7d2.jpg)

Here's the view:

![48-EditPostPage-rendered](https://dev-to-uploads.s3.amazonaws.com/i/wmzu2lgzbv2aoatffa2o.jpg)

# 4.14 `EditPostCell`

We have the `UPDATE_POST_MUTATION` and `QUERY` object types we discussed at the beginning of this article. At the bottom we are again returning the `<PostForm>` component except this time we also have a `post` prop to specify which post is being edited.

![49-web-src-components-EditPostCell](https://dev-to-uploads.s3.amazonaws.com/i/vhut3tz01l71dl3jwn96.jpg)

Here's the view:

![50-EditPostCell-rendered](https://dev-to-uploads.s3.amazonaws.com/i/qdiz1vubwwdf27ivtnif.jpg)

# 4.15 `PostsPage`

In Redwood we use singular "post" when working with a single post object and the data associated with it. When we are working with many posts we use the plural "posts." Here we are displaying all of our posts, so it's called `PostsPage`.

![51-web-src-pages-PostsPage](https://dev-to-uploads.s3.amazonaws.com/i/lnfmzpy7q4ukr3uoqgrx.jpg)

Here's the view:

![52-PostsPage-rendered](https://dev-to-uploads.s3.amazonaws.com/i/7wzcdzu69xwsgus2d1r2.jpg)

# 4.16 `PostsCell`

![53-web-src-components-PostsCell](https://dev-to-uploads.s3.amazonaws.com/i/kjgnfqrdujdyrq3vuvj2.jpg)

Here's the view if you have no posts:

![54-posts-page](https://dev-to-uploads.s3.amazonaws.com/i/amyxsy9qenzoh3o2q8co.jpg)

# 4.17 `Posts`

![55-web-src-components-Posts](https://dev-to-uploads.s3.amazonaws.com/i/snm1sfn10k3zuvwi9nr2.jpg)

`truncate` limits the length of the posts being shown, and `timeTag` encapsulates the logic for created a timestamp for each post.

![56-web-src-components-Posts-PostsList](https://dev-to-uploads.s3.amazonaws.com/i/juwt14splx7gtt33bkus.jpg)

`onCompleted` and `onDeleteClick` are the same functions that we saw in the `NewPost` component.

## `rw-table-wrapper-responsive`

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

## `<thead>`

The table head lets us know the different fields.

![60-Posts-thead](https://dev-to-uploads.s3.amazonaws.com/i/lwnqvinu625el0rkjcb8.jpg)

Here's the view:

![61-Posts-thead-rendered](https://dev-to-uploads.s3.amazonaws.com/i/glbmk5wznlufgel4t4z1.jpg)

## `<tbody>`

In the first half of the table body we map over the data passed through the `post` prop, use the post's `id` for the `key` and then pull out the `id`, `title`, `body`, and `createdAt` time.

![62-Posts-td](https://dev-to-uploads.s3.amazonaws.com/i/i47ffyvrkd8ozjv162io.jpg)

Here's the view:

![63-Posts-td-rendered](https://dev-to-uploads.s3.amazonaws.com/i/11wn58igymraxfee2li3.jpg)

In the second half of the table body we have links to go to a post's page, edit a post, or delete a post.

![64-Posts-rw-table-actions](https://dev-to-uploads.s3.amazonaws.com/i/jz3rfn88x9igohxo412u.jpg)

Here's the view:

![65-Posts-rw-table-actions-rendered](https://dev-to-uploads.s3.amazonaws.com/i/834jvs58ynt6vz1exwou.jpg)

# 4.18 `redwood generate cell`

Now we are going to create a cell that will render the most recent blog posts to the front page.

```
yarn rw g cell BlogPosts
```

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

This doesn't look very good though, I don't think anyone would want to read this blog.

In the `BlogPostsCell` file inside `Success` we can create a component for our posts and give it a little structure.

![74-BlogPostsCell-map-over-posts](https://dev-to-uploads.s3.amazonaws.com/i/3kb5ndh5vxfaodu5kfv0.jpg)

We'll do some more styling later on but for now we have our posts rendered to the front page.

![75-BlogPostsCell-render-map-over-posts](https://dev-to-uploads.s3.amazonaws.com/i/4nion84xg9lco3guqomu.jpg)

In the [next part](https://dev.to/ajcwebdev/a-first-look-at-redwood-js-part-5-2ol4) we'll create a contact form.

# Part 5 - Contact

> *We see it as a Rails replacement. Anything you would normally do with Rails we hope that you’ll be able to do with Redwood.*  
>***Tom Preston-Werner - [Full Stack Radio 138](https://www.fullstackradio.com/episodes/138)***

|Introduction|Tutorial|
|------------|--------|
|[I - Redwood Philosophies](https://dev.to/ajcwebdev/redwood-1d46)|[Part 1 - Setup](https://dev.to/ajcwebdev/a-first-look-at-redwood-js-1017)|
|[II - Full Stack React](https://dev.to/ajcwebdev/full-stack-react-1ihi)|[Part 2 - Routes](https://dev.to/ajcwebdev/a-first-look-at-redwood-js-part-2-44ph)|
|[III - Jamstack](https://dev.to/ajcwebdev/a-short-history-of-the-jamstack-3lk7)|[Part 3 - Prisma](https://dev.to/ajcwebdev/a-first-look-at-redwood-js-part-3-5ao5)|
|[IV - Serverless](https://ajcwebdev.substack.com/p/42-a-short-history-of-serverless)|[Part 4 - CRUD](https://dev.to/ajcwebdev/a-first-look-at-redwood-js-part-4-2m0g)|
||Part 5 - Contact|
||[Part 6 - GraphQL](https://dev.to/ajcwebdev/a-first-look-at-redwood-js-part-6-a25)|
||[Part 7 - Deploy](https://dev.to/ajcwebdev/a-first-look-at-redwood-js-part-7-22b0)|
||[Part 8 - Auth](https://dev.to/ajcwebdev/a-first-look-at-redwood-js-part-8-3pjc)|

If you've made it this far into my series of blog posts I commend you and hope you've found them useful.

In [part 1](https://dev.to/ajcwebdev/a-first-look-at-redwood-js-1017) we created our RedwoodJS app, in [part 2](https://dev.to/ajcwebdev/a-first-look-at-redwood-js-part-2-44ph) we created links between different pages and a reusable layout, in [part 3](https://dev.to/ajcwebdev/a-first-look-at-redwood-js-part-3-5ao5) we got the database up and running and learned CRUD operations for our blog posts, and in [part 4](https://dev.to/ajcwebdev/a-first-look-at-redwood-js-part-4-2m0g) we set up the frontend to query data from the backend to render a list of blog posts to the front page.

In this part we'll be combining everything we've learned up to this point to generate a contact page and take input from a user. We'll be using the same form tags that we learned about in part 4, which are wrappers around [react-hook-form](https://react-hook-form.com/get-started).

This is the simplest way to create a form, but Redwood can be used with other popular React form libraries like Formik or you can use react-hook-form directly.

Forms are a topic I'm particularly passionate about and believe receive far too little attention in bootcamp curriculums and online tutorials. They may not be the most exciting topic, but I encourage you to not gloss over these parts of the framework.

# 5.1 `redwood generate page contact`

The first step is to enter the `yarn redwood generate page` command to create our contact page.

```
yarn rw g page contact
```

![01-generating-page-files](https://dev-to-uploads.s3.amazonaws.com/i/efjyltt08jjalodfq1kv.jpg)

# 5.2 `ContactPage`

This generates a folder called `ContactPage` in our `web/src/pages` folder, and creates two files, `ContactPage.js` and `ContactPage.test.js`.

![02-pages-folder](https://dev-to-uploads.s3.amazonaws.com/i/heo7a47gpiox8pkszypt.jpg)

This should look familiar if you've followed along with the whole series.

![03-ContactPage](https://dev-to-uploads.s3.amazonaws.com/i/lxdfrlp08qke7ksx2wua.jpg)

Our `ContactPage` component contains the same boilerplate we saw when we created our home page and our about page.

![04-ContactPage-rendered](https://dev-to-uploads.s3.amazonaws.com/i/f2qxgmtl87yuiqyygk2z.jpg)

Go to BlogLayout and add a link to the contact page.

![05-routes.contact](https://dev-to-uploads.s3.amazonaws.com/i/ma0nxncbk22gverlbbje.jpg)

Now we'll import `BlogLayout` into `ContactPage.js` and wrap our contact page content in the `BlogLayout` component.

![06-ContactPage-BlogLayout](https://dev-to-uploads.s3.amazonaws.com/i/zpvr47pl8y461f0fkl7y.jpg)

We can now navigate to any of our three pages.

![07-ContactPage-BlogLayout-rendered](https://dev-to-uploads.s3.amazonaws.com/i/p7numdwdrbi2go6kv2ju.jpg)

# 5.3 `Form`

We're going to import the `Form` tags that we looked at in the previous section. Refer to [part 4](https://dev.to/ajcwebdev/a-first-look-at-redwood-js-part-4-2m0g) or the [Redwoodjs docs](https://redwoodjs.com/docs/form) to learn more about these tags.

![08-ContactPage-Form-imports](https://dev-to-uploads.s3.amazonaws.com/i/8lz54b0ty8f34c96fted.jpg)

Now that we've imported the tags, create a `Form` with a `Label` and `TextField` for name, and a `Submit` button.

![09-ContactPage-Form-Label-TextField-Submit](https://dev-to-uploads.s3.amazonaws.com/i/nf45gocqrtbe3ddejsmc.jpg)

Here is the label, input, and button.

![10-ContactPage-Form-rendered](https://dev-to-uploads.s3.amazonaws.com/i/ppovd1eq8kwkkwtj5oub.jpg)

We'll add a little CSS in a moment, but first see what happens if we try to input data.

![11-ContactPage-input](https://dev-to-uploads.s3.amazonaws.com/i/sp1be18nr9iwa82ggccn.jpg)

If we click the save button we'll get an error.

![12-error-message](https://dev-to-uploads.s3.amazonaws.com/i/trce1ompqsf27c3vtcu1.jpg)

This makes sense, we haven't told our form what to do yet with the data. Let's create a function called `onSubmit` that will take in a `data` object and console log the `data` object.

![13-ContactPage-onSubmit](https://dev-to-uploads.s3.amazonaws.com/i/6oic6aja5mw3mo9hrd8l.jpg)

The `onSubmit` prop accepts a function name or anonymous function to be called if validation is successful. This function will be called with a single object containing key/value pairs of all Redwood form helper fields in your form.

![14-ContactPage-Form-onSubmit](https://dev-to-uploads.s3.amazonaws.com/i/0oajg6c4yc14m9hf7y6s.jpg)

Now if enter data into the form and click save we'll see the following in our console:

![15-console.log(data)](https://dev-to-uploads.s3.amazonaws.com/i/h1qrvfwyamgt0iopa81s.jpg)

# 5.4 `data`

Our input is contained in the `data` object. Right now it only has a key/value pair for name but we'll be adding more in a moment.

Before doing that, what can we do with this `data` object?

![16-ContactPage-onSubmit-data.name](https://dev-to-uploads.s3.amazonaws.com/i/fccxgw7plj9ayh7kwlqu.jpg)

We can pull out the value of name by console logging `data.name`:

![17-console.log(data.name)](https://dev-to-uploads.s3.amazonaws.com/i/osd91p0akqcwzss0adbi.jpg)

We want to be able to accept a longer message from our users, so we're going to import the `TextAreaField` tag.

![18-ContactPage-TextAreaField-import](https://dev-to-uploads.s3.amazonaws.com/i/bxjbchhvok6ev3z7hnun.jpg)

We now how a `TextField` for name and email, and a `TextAreaField` for a message.

![19-ContactPage-email-message](https://dev-to-uploads.s3.amazonaws.com/i/pbgp8rlbbp74s4swtep1.jpg)

To make this look a little nicer we're going to include just a little CSS.

![20-index.css](https://dev-to-uploads.s3.amazonaws.com/i/uwe7gw6m73e87x3j3xba.jpg)

Our buttons, inputs, and labels are now `display: block` which adds a line break after any appearance of these tags, and the label also has a little bit of margin on the top.

![21-ContactPage-email-message-rendered](https://dev-to-uploads.s3.amazonaws.com/i/uel9h6fybf0atj6oraac.jpg)

We'll test out all the fields:

![22-ContactPage-email-message-input](https://dev-to-uploads.s3.amazonaws.com/i/hkwqxkywjx0ff19o6onj.jpg)

We now are getting back an object with three key/value pairs.

![23-ContactPage-email-message-console.log](https://dev-to-uploads.s3.amazonaws.com/i/39xsmt7mee7rxbd81xo2.jpg)

We can console log any part of the object that we want.

![24-data.email-data.message](https://dev-to-uploads.s3.amazonaws.com/i/u9rel43i5oba9st2i1ch.jpg)

Now if we look at our console we'll see each output and it even tells us which file and line corresponds to each piece of data.

![25-data.email-data.message-console.log](https://dev-to-uploads.s3.amazonaws.com/i/ess2h63bpmrvb7g88mk7.jpg)

# 5.5 `validation`

What happens if we only fill out some of the form and try to submit?

![26-just-name-input](https://dev-to-uploads.s3.amazonaws.com/i/g2m7m1si3o4szb7f8c3k.jpg)

The form doesn't care, it simply takes the empty inputs and returns an empty string.

![27-empty-email-message](https://dev-to-uploads.s3.amazonaws.com/i/yb6fweldvgf1oep19qth.jpg)

We want to add some validation so the user can't submit the form unless they've given input for all three fields.

![28-errorClassName-validation](https://dev-to-uploads.s3.amazonaws.com/i/thrzvua73d8tpusegf1t.jpg)

# 5.6 `errorClassName`

We gave each `TextField` an `errorClassName` with the attribute `error`. The `validation` prop accepts an object containing options for react-hook-form.

Right now we're just adding the `required` attribute, but later we'll use the `validation` prop for a regular expression.

![29-input.error-textarea.error-label.error](https://dev-to-uploads.s3.amazonaws.com/i/kxzghajegp77zgihm5w2.jpg)

In our CSS we'll add the following properties for errors.

![30-textfield-errors](https://dev-to-uploads.s3.amazonaws.com/i/89h31o7q5gznshyn9evc.jpg)

Now when we try to submit an empty field we see the color change to red.

![31-textfield-errors-with-name](https://dev-to-uploads.s3.amazonaws.com/i/62498bbmd3l2pm755566.jpg)

Once we give input the red error color goes away.

![32-invalid-email](https://dev-to-uploads.s3.amazonaws.com/i/qcvdmkctrawzwdk3mce7.jpg)

There's still an issue, which is we can submit an email that is invalid.

![33-email-regex](https://dev-to-uploads.s3.amazonaws.com/i/vhufd6wnxfkqbeoboqec.jpg)

Here's a regular expression provided in the Redwood tutorial video. Don't ask me to explain it, cause I don't know what it's doing.

All I know is it does a thing with the `@` symbol, then it does another thing with the `.` symbol, then it does some other things and figures out if you gave an email or not. Google "regex tutorials" if that wasn't a satisfactory explanation for you. 

![34-email-error](https://dev-to-uploads.s3.amazonaws.com/i/qbue5djgy4zkdh607c2g.jpg)

# 5.7 `FieldError`

Now we get an error if we don't provide a valid email address. It would really be nice if we could tell our user why they are getting an error.

![35-import-FieldError](https://dev-to-uploads.s3.amazonaws.com/i/k1qri4wptsgkzec8nqt9.jpg)

We're going to import `FieldError` to show error messages to our users.

![36-FieldError-name-email-message](https://dev-to-uploads.s3.amazonaws.com/i/z1jgch5tzcjkx936rm0t.jpg)

Now if we try to submit without giving input we are told that the field is required.

![37-name-email-message-required](https://dev-to-uploads.s3.amazonaws.com/i/id3eran7gi9oh9cvkvvj.jpg)

If we enter an invalid email we are told that the email is not formatted correctly.

![38-email-formatted-incorrectly](https://dev-to-uploads.s3.amazonaws.com/i/deuyijhto9quyq4h6081.jpg)

If we add the `errorClassName` to the `Label` tags we'll also turn the labels red if there's an error.

![39-label-errorClassName](https://dev-to-uploads.s3.amazonaws.com/i/ni5hx5xfpb0v99l1sdyv.jpg)

Now we have the label and the input field turn red if there's an error.

![40-label-errors](https://dev-to-uploads.s3.amazonaws.com/i/nwejvnxof46j8hzo922x.jpg)

Might as well make everything red while we're at it.

![41-FieldError-style-red](https://dev-to-uploads.s3.amazonaws.com/i/aukmo67p6tdj56ax21i1.jpg)

Since the `FieldError` will only show on errors we can just inline styles with `style={{ color: 'red' }}`.

![42-all-red](https://dev-to-uploads.s3.amazonaws.com/i/gdiqd3h5abb2d7h5zz7i.jpg)

Glorious red as far as the eye can see. Something's still not right though. "Message is required" should be on its own line.

![43-message-error-display-block](https://dev-to-uploads.s3.amazonaws.com/i/1akdzjrp4w4inkprrbiy.jpg)

Adding `display: 'block'` will put the error on its own line.

![44-message-error-display-block-rendered](https://dev-to-uploads.s3.amazonaws.com/i/rpnvykfbmx2nn08nbblp.jpg)

It would also be nice if we could tell the user a field is required before they hit the submit button. We'll do that by adding `mode: 'onBlur'` and pass that into `validation`.

![45-form-validation-mode-onBlur](https://dev-to-uploads.s3.amazonaws.com/i/8juv4snet5lcfjhvakk7.jpg)

Now when we enter a field and leave without filling it out we are immediately given feedback.

![46-form-validation-mode-onBlur-rendered](https://dev-to-uploads.s3.amazonaws.com/i/4lbt7ci62w5js29g6hdr.jpg)

And for now that's our entire form. Here's a look at all the form code.

![47-entire-form](https://dev-to-uploads.s3.amazonaws.com/i/1kay4suc8augz4a1ix84.jpg)

In the [next part](https://dev.to/ajcwebdev/a-first-look-at-redwood-js-part-6-a25) we'll connect our contact form to our database so we can persistent the data entered into the form.

# Part 6 - GraphQL

>*GraphQL becomes the one and only mediator between your frontend and your backend.*  
>***Tom Preston-Werner - [RedwoodJS with Tom Preston-Werner](https://www.softwaredaily.com/post/5ec7997912b353000c6381d8/RedwoodJS-with-Tom-PrestonWerner)***

|Introduction|Tutorial|
|------------|--------|
|[I - Redwood Philosophies](https://dev.to/ajcwebdev/redwood-1d46)|[Part 1 - Setup](https://dev.to/ajcwebdev/a-first-look-at-redwood-js-1017)|
|[II - Full Stack React](https://dev.to/ajcwebdev/full-stack-react-1ihi)|[Part 2 - Routes](https://dev.to/ajcwebdev/a-first-look-at-redwood-js-part-2-44ph)|
|[III - Jamstack](https://dev.to/ajcwebdev/a-short-history-of-the-jamstack-3lk7)|[Part 3 - Prisma](https://dev.to/ajcwebdev/a-first-look-at-redwood-js-part-3-5ao5)|
|[IV - Serverless](https://ajcwebdev.substack.com/p/42-a-short-history-of-serverless)|[Part 4 - CRUD](https://dev.to/ajcwebdev/a-first-look-at-redwood-js-part-4-2m0g)|
||[Part 5 - Contact](https://dev.to/ajcwebdev/a-first-look-at-redwood-js-part-5-2ol4)|
||Part 6 - GraphQL|
||[Part 7 - Deploy](https://dev.to/ajcwebdev/a-first-look-at-redwood-js-part-7-22b0)|
||[Part 8 - Auth](https://dev.to/ajcwebdev/a-first-look-at-redwood-js-part-8-3pjc)|

In [part 5](https://dev.to/ajcwebdev/a-first-look-at-redwood-js-part-5-2ol4) we generated a contact page and took input from the user. In this part we'll connect our contact form to our database so we can persist the data entered into the form.

# 6.1 `Contact`

To modify our database we'll go to our `schema.prisma` file and add a `Contact` model.

![01-Contact-model](https://dev-to-uploads.s3.amazonaws.com/i/rik97onoi44q4khfy2im.jpg)

The [model](https://www.prisma.io/docs/reference/tools-and-interfaces/prisma-schema/data-model) takes the `name`, `email`, and `message` strings from the form inputs. It creates an `id` with `autoincrement()` and `createdAt` time with [`now()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Date/now).

Enter `yarn redwood db save` to create a migration schema.

```
yarn rw db save
```

It will automatically assign your migration a name.

![02-name-of-migration](https://dev-to-uploads.s3.amazonaws.com/i/u5azp2t2dnflvdso0iaw.jpg)

This will create another `migrations` directory with a schema file, README, and `steps.json` file like we saw in [part 3](https://dev.to/ajcwebdev/a-first-look-at-redwood-js-part-3-5ao5).

![03-migrate-save--name](https://dev-to-uploads.s3.amazonaws.com/i/b3pyqs6hduccj5nosrf7.jpg)

Enter `yarn redwood db up` to apply that migration to the database.

```
yarn rw db up
```

This will output the database actions applied after the migration, which includes one `CreateTable` statement.

![04-migrate-up](https://dev-to-uploads.s3.amazonaws.com/i/nqe7nkgn0x8k9xf6qbl8.jpg)

Lastly the [Prisma Client](https://www.prisma.io/docs/reference/tools-and-interfaces/prisma-client) is generated.

![05-generate-Prisma-client](https://dev-to-uploads.s3.amazonaws.com/i/cmgf9zzve0025xi50y24.jpg)

# 6.2 `redwood generate sdl`

Enter `yarn redwood generate sdl contact` to create the schema definition language for the contact form.

```
yarn rw g sdl contact
```

This will create an sdl in your `graphql` folder and a resolver in your `services` folder.

![06-generating-SDL-files](https://dev-to-uploads.s3.amazonaws.com/i/ned1ofbjuk6o87xckqp8.jpg)

We created three files:
* `contacts.sdl.js` in the `graphql` folder
* `contacts.js` in the `services/contacts` folder
* `contacts.test.js` in the `services/contacts` folder

![07-api-src-folder](https://dev-to-uploads.s3.amazonaws.com/i/mtos8csbkgarchjy4nox.jpg)

# 6.3 `contacts.sdl.js`

We'll look at our schema definition language first.

![08-contacts.sdl.js](https://dev-to-uploads.s3.amazonaws.com/i/rq4mhu4gvt4q1m306h55.jpg)

The sdl has two types:
* `Contact`
* `Query`

And two inputs:
* `CreateContactInput`
* `UpdateContactInput`

# 6.4 `createContact`

We need to create our own mutation. We don't get this by default because the sdl generator doesn't know what we plan to do with the schema.

![09-type-Mutation](https://dev-to-uploads.s3.amazonaws.com/i/9vqfxkrqdhovhq4hxbrx.jpg)

Our `Mutation` type will be called `createContact`. The input is `CreateContactInput!` and it returns `Contact`.

# 6.5 `contacts.js`

Now we'll look at our `contacts` service. It has a resolver for the `Query` type from our sdl.

![10-contacts.js](https://dev-to-uploads.s3.amazonaws.com/i/n84yisnvoec42ritha4x.jpg)

We'll create a resolver for `createContact`.

![11-createContact-resolver](https://dev-to-uploads.s3.amazonaws.com/i/6yxjn6pywwwxm9az20cv.jpg)

This takes `input` from the browser and adds it to the database.

# 6.6 `CREATE_CONTACT`

In our `ContactPage` file we'll add the mutation and assign it to `CREATE_CONTACT`. It is a common convention to use all caps for our mutations.

![12-CREATE_CONTACT-mutation](https://dev-to-uploads.s3.amazonaws.com/i/9k08w198bmlof9j3zy8t.jpg)

We will just return the `id` since the user will not see this.

Make sure to import `useMutation` at the top of the file.

![13-import-useMutation](https://dev-to-uploads.s3.amazonaws.com/i/hutydwj35iwe3m3xj3jw.jpg)

Inside the `ContactPage` component we'll call `useMutation()`. We pass an object `create` with variables that are defined in `CREATE_CONTACT`.

![14-useMutation](https://dev-to-uploads.s3.amazonaws.com/i/e4pnifj41gnufq56u9ue.jpg)

The input is the actual object containing the `data` which is assigned to `variables` and passed to the `create()` function inside `onSubmit`.

We are now ready to enter our data. Enter a name, email, and message and click the Save button.

![15-form-input](https://dev-to-uploads.s3.amazonaws.com/i/kjzs5a7m4e086ullmreo.jpg)

Our form gives us the following object which we saw in the previous part.

![16-form-input-console-log](https://dev-to-uploads.s3.amazonaws.com/i/4z7jry0ch4sgdy5ibzn6.jpg)

# 6.7 `graphiQL`

We can now check to make sure it was saved. Remember all the way back in part 1 when we said there was something else running on `localhost:8911`?

![17-localhost-8911](https://dev-to-uploads.s3.amazonaws.com/i/1zhyxon1bkt73nyp26zr.jpg)

This is how we access the graphiQL interface. Click the graphql link.

![18-graphiQL](https://dev-to-uploads.s3.amazonaws.com/i/512op701y527bb8offur.jpg)

GraphiQL is like an IDE for your GraphQL queries. On the left side you'll enter a query, and after clicking the middle play button the response will appear on the right side.

We'll create a `contact` query that will return all the `contacts` in the database.

![19-contact-query](https://dev-to-uploads.s3.amazonaws.com/i/j7h868bqktmqm8x98lz8.jpg)

We'll ask for the `id`, `name`, `email`, and `message`.

Click the play button and on the right side you'll receive a `data` object containing whatever your entered into your form.

![20-contact-data](https://dev-to-uploads.s3.amazonaws.com/i/pp55ohfrk4pdeir1aamf.jpg)

The `data` object contains a `contacts` array with objects containing the form input.

There's a few more things we can add to our form to make the user experience a little better.
1. We want to give the user some immediate feedback after they click the save button.
2. We also want to put in safeguards in case the user feels like clicking the save button many times in fast succession.

# 6.8 `loading`

To do this we'll add a `loading` object after `create`.

![21-loading](https://dev-to-uploads.s3.amazonaws.com/i/whsrnlz3p0k50dtzhiqo.jpg)

`loading` will be true while the mutation is being performed, and will change to false when the mutation is complete.

We will add `disabled` to the `Submit` button and pass it the `loading` object.

![22-Submit-disabled-loading](https://dev-to-uploads.s3.amazonaws.com/i/1rnrjklfzzwhyquzwopj.jpg)

While the mutation is in progress disabled is true, and once it is complete it will change to false. To test this out go to your Network tab in your browsers devtools. Here we can simulate slow 3G.

![23-slow-3G](https://dev-to-uploads.s3.amazonaws.com/i/nj3ubs2v4ptbp6okikta.jpg)

Enter some more data and click the Save button.

![24-save-button-greyed-out](https://dev-to-uploads.s3.amazonaws.com/i/xm2ykilh8nvwlcmlsqjr.jpg)

Now when you click the Save button it will be greyed out for a moment while the input is saved to the database.

# 6.9 `useForm`

Another problem with this form is the input sticks around on the page even after it is submitted. It would be better if we cleared the fields after submitting. We can do this by importing `useForm` from `react-hook-form`.

![25-import-useForm](https://dev-to-uploads.s3.amazonaws.com/i/myz40eabl6v20wddq427.jpg)

Inside our `ContactPage` component we'll create a `formMethods` variable and assign it the `useForm()` function that we just imported.

![26-formMethods](https://dev-to-uploads.s3.amazonaws.com/i/uu2wnodut3xr0be84u1h.jpg)

Inside `<Form>` we'll add `formMethods` and pass it `formMethods` as a prop.

![27-Form-formMethods](https://dev-to-uploads.s3.amazonaws.com/i/unp5aapyrqcr6amiui1b.jpg)

This gives us access to the reset function. In `useMutation` we'll add a second parameter, which is a callback called `onCompleted`.

![28-onCompleted](https://dev-to-uploads.s3.amazonaws.com/i/jh8j06e9wzez42oxt9ai.jpg)

When the mutation is complete we'll call `formMethods.reset()` and display an `alert()` saying `Thanks for telling me stuff about my things!` To test this in the browser, enter some more data and click the Save button.

![29-alert-thanks-for-the-message](https://dev-to-uploads.s3.amazonaws.com/i/ttuy2eu9b30735ggvyt7.jpg)

First the alert message appears on the screen. After clicking OK the form will be cleared.

![30-form-cleared](https://dev-to-uploads.s3.amazonaws.com/i/hl362fprnvvy4vp8qfco.jpg)

Another thing we can improve is the label. Right now it is just defaulting to whatever is entered as the `name` attribute in `<Label>`. We can add a closing `</Label>` tag and enter something between the tags to change the label. We'll capitalize the labels.

![31-Name-label](https://dev-to-uploads.s3.amazonaws.com/i/hxmhd9cuhxywbz184xr3.jpg)

![32-Email-label](https://dev-to-uploads.s3.amazonaws.com/i/pfnpwubw35jlkx2v7d7s.jpg)

![33-Message-label](https://dev-to-uploads.s3.amazonaws.com/i/8huz2db0bq969ml62epm.jpg)

Check your form for the changes.

![34-updated-form-labels](https://dev-to-uploads.s3.amazonaws.com/i/gdahhgdkodvp3ct0oodl.jpg)

In the [next part](https://dev.to/ajcwebdev/a-first-look-at-redwood-js-part-7-22b0) we'll finally deploy our project to the internet with Netlify and Heroku.

# Part 7 - Deploy

>*RedwoodJS is an attempt to build a full stack framework for JavaScript and to really deploy it in a serverless way. So that’s one of the primary tenants that we have:*
>
>*Build it end to end with JavaScript. Deploy it to a serverless environment to give you the advantages of the scale that that can bring as well as the global distribution that that can bring.*  
>***Tom Preston-Werner - [Full Stack Radio 138](https://www.fullstackradio.com/episodes/138)***

|Introduction|Tutorial|
|------------|--------|
|[I - Redwood Philosophies](https://dev.to/ajcwebdev/redwood-1d46)|[Part 1 - Setup](https://dev.to/ajcwebdev/a-first-look-at-redwood-js-1017)|
|[II - Full Stack React](https://dev.to/ajcwebdev/full-stack-react-1ihi)|[Part 2 - Routes](https://dev.to/ajcwebdev/a-first-look-at-redwood-js-part-2-44ph)|
|[III - Jamstack](https://dev.to/ajcwebdev/a-short-history-of-the-jamstack-3lk7)|[Part 3 - Prisma](https://dev.to/ajcwebdev/a-first-look-at-redwood-js-part-3-5ao5)|
|[IV - Serverless](https://ajcwebdev.substack.com/p/42-a-short-history-of-serverless)|[Part 4 - CRUD](https://dev.to/ajcwebdev/a-first-look-at-redwood-js-part-4-2m0g)|
||[Part 5 - Contact](https://dev.to/ajcwebdev/a-first-look-at-redwood-js-part-5-2ol4)|
||[Part 6 - GraphQL](https://dev.to/ajcwebdev/a-first-look-at-redwood-js-part-6-a25)|
||Part 7 - Deploy|
||[Part 8 - Auth](https://dev.to/ajcwebdev/a-first-look-at-redwood-js-part-8-3pjc)|

In this [penultimate](https://www.merriam-webster.com/dictionary/penultimate) part we will:
* Deploy our frontend application with Serverless functions on Netlify
* Deploy our backend to a hosted Postgres database on Heroku

# 7.1 GitHub Repo

First you will need a GitHub repo with your Redwood project. Mine is [here](https://github.com/ajcwebdev/ajcwebdev/). It contains branches that match up with the state of the project at the end of each of the first six parts. The default branch is part7 and will be the branch we deploy.

![01-github-repo](https://dev-to-uploads.s3.amazonaws.com/i/ttr1wngw4q6j0ztrpmd7.jpg)

# 7.2 Netlify

```bash
yarn rw g deploy netlify
```

![02-yarn-generate-deploy-netlify](https://dev-to-uploads.s3.amazonaws.com/i/f1rlw09ce8ka0g85nksf.jpg)

This creates a file at `/netlify.toml` containing the commands and file paths that Netlify needs to know about to build a Redwood app.

![03-netlify.toml](https://dev-to-uploads.s3.amazonaws.com/i/bp995mogzb5expuhgsm9.jpg)

Next you'll need an account on [Netlify](http://netlify.com/).

![04-netlify-sites](https://dev-to-uploads.s3.amazonaws.com/i/0ae0i5yvfydgmlq2yg3g.jpg)

Click `New site from Git` to create a new site from git.

![05-new-site-from-git](https://dev-to-uploads.s3.amazonaws.com/i/k5va79ftlji8n8pgyqn3.jpg)

You can also use GitLab or Bitbucket. 

![06-create-a-new-site](https://dev-to-uploads.s3.amazonaws.com/i/hke4rkg7c25o0ylhqhu6.jpg)

Enter the name of your repo into the search bar.

![07-ajcwebdev-repo](https://dev-to-uploads.s3.amazonaws.com/i/gj0unavsfx7as0jh1iq2.jpg)

Select the repo.

![08-ajcwebdev/ajcwebdev](https://dev-to-uploads.s3.amazonaws.com/i/98n6n2564hlizskaqxwu.jpg)

It selects the default branch to deploy.

![09-branch-to-deploy](https://dev-to-uploads.s3.amazonaws.com/i/3idt3g6rvzspzvpx7z9g.jpg)

The build command may be entered by default.

![10-build-command](https://dev-to-uploads.s3.amazonaws.com/i/it7b79zxdyozz9slpqfe.jpg)

If the build command is blank enter the following:

```bash
yarn rw build && yarn rw db up --no-db-client --auto-approve && yarn rw dataMigrate up
```

Click `Deploy site` to deploy the site.

![11-site-deploy-in-progress](https://dev-to-uploads.s3.amazonaws.com/i/up5prlddtk9iiarv40ij.jpg)

If we go to the `Deploys` section we can see more information about the build.

![12-netlify-deploys](https://dev-to-uploads.s3.amazonaws.com/i/51r5znou958rtvrnglck.jpg)

Your build should take at least a minute or more, so don't freak out if it doesn't work immediately.

![13-deploy-published](https://dev-to-uploads.s3.amazonaws.com/i/6ovc5rl1dgistuphh93w.jpg)

Our deploy took 2 minutes and 15 seconds and we can also see a summary of the deploy.

![14-deploy-summary](https://dev-to-uploads.s3.amazonaws.com/i/tqf4gcnce5fr5vbw0j0x.jpg)

We haven't really deployed the site though, because right now we just have the frontend deployed to Netlify. But we haven't done anything with our database so we should expect an error:

![15-error-unexpected-token](https://dev-to-uploads.s3.amazonaws.com/i/oqil2vvnzn2nffpf9ljw.jpg)

# 7.3 Heroku

To get our database online we'll need to set up another account and project on [Heroku](heroku.com).

![16-heroku-apps](https://dev-to-uploads.s3.amazonaws.com/i/2q0t1aqwqn6988wpkev2.jpg)

If this is your first project you can click the `Create new app` button in the middle to create a new app or you can click the `New` button on the top right.

![17-create-new-app](https://dev-to-uploads.s3.amazonaws.com/i/vw15vd439zqqtxp5jro6.jpg)

We'll give the app the same name as the Github repo.

![18-app-name-ajcwebdev](https://dev-to-uploads.s3.amazonaws.com/i/rn0nb2tu3e2w6hn5oj9t.jpg)

Now we have a dashboard for our project much like we did in Netlify.

![19-heroku-deploy](https://dev-to-uploads.s3.amazonaws.com/i/kcz8vpv2dubbdjbfe400.jpg)

Lets take a look at our `Resources` tab so we can provision our database.

![20-heroku-resources](https://dev-to-uploads.s3.amazonaws.com/i/bsspznyekikwp5ykb8va.jpg)

Click `Find more add-ons` to find more add-ons.

![21-find-more-add-ons](https://dev-to-uploads.s3.amazonaws.com/i/iiloqno840koo34sh8vl.jpg)

There are many add-ons. We only need one, Heroku Postgres. Why Postgres? [Because Postgres is the best database; there is no other database](https://www.heavybit.com/library/podcasts/jamstack-radio/ep-35-graphql-querying-with-hasuras-tanmai-gopal/).

![22-heroku-postgres](https://dev-to-uploads.s3.amazonaws.com/i/opa5syr4igu12lzybb7x.jpg)

Click `Install Heroku Postgres` to install Heroku Postgres.

![23-install-heroku-postgres](https://dev-to-uploads.s3.amazonaws.com/i/iqkc8u5w9ku2l9h0zqyy.jpg)

You can select your add-on plan, we'll be using the free option.

![24-provision-add-on](https://dev-to-uploads.s3.amazonaws.com/i/jtc3jh4e44cbncuw2apu.jpg)

Enter the name of your heroku app and it should appear in the autocomplete.

![25-app-to-provision-to](https://dev-to-uploads.s3.amazonaws.com/i/pnz7t87xknbmd2juxdb5.jpg)

Select your project and click `Provision add-on` to provision the add-on.

![26-click-provision-add-on-button](https://dev-to-uploads.s3.amazonaws.com/i/trg087x8p3ap259mkpf1.jpg)

Now our database is installed.

![27-app-provisioned](https://dev-to-uploads.s3.amazonaws.com/i/vq4q9dk3kddee29vii8m.jpg)

# 7.4 Config/Environment Variables

Lets go to the `Settings` tab so we can connect this database to our frontend. Click `Reveal Config Vars` to reveal the config variables.

![28-heroku-settings](https://dev-to-uploads.s3.amazonaws.com/i/89eall7eshul9v3jpk51.jpg)

We can see a key/value pair for the database URL, normally it wouldn't be wise to share environment variables online, but this project is purely explanatory and won't be holding any sensitive data.

![29-enter-config-vars](https://dev-to-uploads.s3.amazonaws.com/i/h851tvjmkn1k8nuci0h8.jpg)

Select the value and copy it to your clipboard. We'll be using this back in our Netlify project.

![30-copy-postgres-vars](https://dev-to-uploads.s3.amazonaws.com/i/tdbwdkrtuhovjv7j71qr.jpg)

Select `Deploy settings` to go to your deploy settings.

![31-netlify-deploys](https://dev-to-uploads.s3.amazonaws.com/i/l7314ljzh8uf6u5vgt0o.jpg)

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

It will be called `BINARY_TARGET` with the value `rhel-openssl-1.0.x`.

![39-BINARY_TARGET](https://dev-to-uploads.s3.amazonaws.com/i/i36b0ueh2ie3rnp2tq2t.jpg)

This is a setting for Prisma which needs to know how to generate the client libraries to access the database. Usually it can auto detect that. However, in this case the libraries that are being built on Netlify are running on Ubuntu.

The API deployed to AWS Lambda is running a flavor of RedHat Enterprise Linux. We need to let Prisma know to build for RedHat and not for Ubuntu.

![40-save-variables](https://dev-to-uploads.s3.amazonaws.com/i/wk7akue4m5mxm3a1l459.jpg)

If we go back to our code in `schema.prisma` we can see that we set our datasource to the environment variable `DATABASE_URL` and our client to `native`.

![41-schema-datasource-generator](https://dev-to-uploads.s3.amazonaws.com/i/5fd9gf4ghozi5dwn657o.jpg)

And then Prisma looks up our local environment file. We override these once you deploy to Netlify.

![42-env.defaults](https://dev-to-uploads.s3.amazonaws.com/i/h2wq6qmb1q7tdb88kb1b.jpg)

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

In the [next and final part](https://dev.to/ajcwebdev/a-first-look-at-redwood-js-part-8-3pjc) we'll add authentication to our application, something that has never confused any developer ever.

# Part 8 - Auth

You made it to the last part!

![Alt Text](https://dev-to-uploads.s3.amazonaws.com/i/jewl54ynr64v8hkfbugb.gif)

Unfortunately I do not have any epic Tom quotes about authentication.

|Introduction|Tutorial|
|------------|--------|
|[I - Redwood Philosophies](https://dev.to/ajcwebdev/redwood-1d46)|[Part 1 - Setup](https://dev.to/ajcwebdev/a-first-look-at-redwood-js-1017)|
|[II - Full Stack React](https://dev.to/ajcwebdev/full-stack-react-1ihi)|[Part 2 - Routes](https://dev.to/ajcwebdev/a-first-look-at-redwood-js-part-2-44ph)|
|[III - Jamstack](https://dev.to/ajcwebdev/a-short-history-of-the-jamstack-3lk7)|[Part 3 - Prisma](https://dev.to/ajcwebdev/a-first-look-at-redwood-js-part-3-5ao5)|
|[IV - Serverless](https://ajcwebdev.substack.com/p/42-a-short-history-of-serverless)|[Part 4 - CRUD](https://dev.to/ajcwebdev/a-first-look-at-redwood-js-part-4-2m0g)|
||[Part 5 - Contact](https://dev.to/ajcwebdev/a-first-look-at-redwood-js-part-5-2ol4)|
||[Part 6 - GraphQL](https://dev.to/ajcwebdev/a-first-look-at-redwood-js-part-6-a25)|
||[Part 7 - Deploy](https://dev.to/ajcwebdev/a-first-look-at-redwood-js-part-7-22b0)|
||Part 8 - Auth|

We're going to implement a login form so no one can edit our blog willy-nilly. But before we do that let's give ourselves a custom domain. We can do this in our Settings on Netlify.

![01-netlify-settings](https://dev-to-uploads.s3.amazonaws.com/i/k8b0eggbgpnnhxivsugr.jpg)

Go to Domain management and you should see a box for Custom domains.

![02-custom-domains](https://dev-to-uploads.s3.amazonaws.com/i/7p33rzro0uvqp1vdxyyq.jpg)

Netlify assigns a random domain name by default but gives the option to edit it.

![03-change-site-name](https://dev-to-uploads.s3.amazonaws.com/i/pmiu3qoa77l36epvxnxp.jpg)

I'll change my site name to `ajcwebdev-redwood`.

![04-ajcwebdev-redwood-netlify-app](https://dev-to-uploads.s3.amazonaws.com/i/lyhldf9h1ugjwave5vx9.jpg)

Click Save and it'll reflect your new site name.

![05-default-subdomain](https://dev-to-uploads.s3.amazonaws.com/i/hdljrrgq5g7yre3a8wbd.jpg)

# 8.1 Netlify Identity

Now lets go to the Identity tab.

![06-netlify-identity](https://dev-to-uploads.s3.amazonaws.com/i/qgg3ny0rgl7wsdp6818c.jpg)

Click `Enable Identity` to enable identity.

![07-netlify-identity-level-0](https://dev-to-uploads.s3.amazonaws.com/i/fjgpii8n9mmvtsdp083n.jpg)

Here we can invite users to give them permissions. We are going to lock down our site and only give ourselves permission to see or edit anything. Click `Invite user` to invite a user.

![08-invite-users](https://dev-to-uploads.s3.amazonaws.com/i/md0mzxm5jw9zrrtak2nu.jpg)

# 8.2 `redwood generate auth`

We'll come back to that, but first we're going to learn one more `redwood generate` command, this time for authentication.

```
yarn rw g auth netlify
```

I'm going to use Netlify but as of now we have the option to use:
* [Netlify Identity](https://docs.netlify.com/visitor-access/identity/)
* [Auth0](https://auth0.com/)
* [Magic Link](https://docs.magic.link/welcome)

This will create an `auth.js` file in `api/src/lib` and automatically modify our `index.js` file in `web/src` and our `graphql.js` file in `api/src/functions`.

![10-redwood-genearte-auth-netlify-output](https://dev-to-uploads.s3.amazonaws.com/i/53iq4s8z1n13y167i6kl.jpg)

If we check our `package.json` file in our `web` folder we'll see two new dependencies `@redwoodjs/auth` and `netlify-identity-widget`.

![11-dependencies-redwood-auth-netlify-identity-widget](https://dev-to-uploads.s3.amazonaws.com/i/0lhp3g6agt8wkvpnrq3k.jpg)

# 8.3 `auth.js`

The `auth.js` file was generated in our `api/src` folder.

![12-lib-auth.js](https://dev-to-uploads.s3.amazonaws.com/i/y2ho6mvb8ijdwh6l6irp.jpg)

Lets look at the generated file.

![13-auth.js](https://dev-to-uploads.s3.amazonaws.com/i/5xnylp6avc3ve9ydtle0.jpg)

# 8.4 `requireAuth`

We have a helper method `requireAuth` which we'll use in our services. If someone is not authenticated it will throw an error.

![14-index.js-netlify-identity](https://dev-to-uploads.s3.amazonaws.com/i/7bguinfxurg6vyvobcu1.jpg)

# 8.5 `AuthProvider`

`AuthProvider` and `netlifyIdentity` are imported. Netlify identity is initialize with `netlifyIdentity.init()`. This will be unique to whatever provider you use.

`AuthProvider` wraps the Router and takes in a `client` and `type` which are `netlifyIdentity` and `netlify` respectively.

![15-graphql.js-getCurrentUser](https://dev-to-uploads.s3.amazonaws.com/i/608jer42ndraueuxo785.jpg)

`getCurrentUser` is imported and passed to the `handler` that sets up our GraphQL so we don't have to worry about it.

![16-posts.js-import-requireAuth](https://dev-to-uploads.s3.amazonaws.com/i/up1g48ccibsrt456oh04.jpg)

We'll import `requireAuth` and use it to restrict access to our endpoints.

![17-requireAuth()](https://dev-to-uploads.s3.amazonaws.com/i/4qnfha11ikd42z8nxee3.jpg)

We want to restrict access to the sensitive endpoints including `createPost`, `updatePost`, and `deletePost`.

![18-test-new-post](https://dev-to-uploads.s3.amazonaws.com/i/j5jayhvnq8ksx7oir0ps.jpg)

Lets try to make a new post.

![19-don't-have-permission-to-make-new-post](https://dev-to-uploads.s3.amazonaws.com/i/0odsc2xc7ijj8xfumf3f.jpg)

# 8.6 `Private`

We are told that we don't have permission to do that. But we want to make it so an unauthenticated user can't even get this far. Let's create private routes for all the `/posts` routes.

![20-import-Private-from-router](https://dev-to-uploads.s3.amazonaws.com/i/ued4vdeue1rq3uftukga.jpg)

We'll import `Private` from `@redwoodjs/router` and use it to wrap our `/posts` routes.

![21-Private-routes-posts](https://dev-to-uploads.s3.amazonaws.com/i/7i0ci5lvqk51fa102pii.jpg)

If we go back to the `new` route we'll now get an error message.

![22-something-went-wrong](https://dev-to-uploads.s3.amazonaws.com/i/5pcsziq7mn2875k4qam5.jpg)

Instead of just showing an error message, we can redirect the user back to the home page by adding `unauthenticated="home"`.

![23-Private-unauthenticated-home-redirect](https://dev-to-uploads.s3.amazonaws.com/i/xs6yvks02mdszx3hck29.jpg)

Now we'll see a redirect in the URL and we'll be taken back to the home

![25-redirect-to-home-page](https://dev-to-uploads.s3.amazonaws.com/i/1lkg2p4flr14rj7odq7p.jpg)

# 8.7 `useAuth`

To implement authentication we'll start by importing `useAuth` from the Redwood `auth` package.

![26-BlogLayout.js-import-useAuth-from-auth](https://dev-to-uploads.s3.amazonaws.com/i/cetywo5g3k016i22pxnq.jpg)

We'll use object destructuring to pull out the `logIn` object.

![27-logIn-destructuring-useAuth()](https://dev-to-uploads.s3.amazonaws.com/i/3sy05ojscvheq11pd374.jpg)

We'll then add a link to Log In and pass the `logIn` object to the `onClick` event handler.

![28-a-href-onClick-logIn](https://dev-to-uploads.s3.amazonaws.com/i/5ahpwwnavbyzbexf9saz.jpg)

If we return to our browser we'll now see a link to log in.

![29-home-page-with-log-in-link](https://dev-to-uploads.s3.amazonaws.com/i/t9bnxguhqw4fynl3bioh.jpg)

If we click the link we'll get this fancy looking message from Netlify asking for our site's url.

![30-url-of-your-netlify-site](https://dev-to-uploads.s3.amazonaws.com/i/24kk3h89pbsjd4sgc4uf.jpg)

Enter the domain that we created at the beginning of the article.

![31-set-site's-url](https://dev-to-uploads.s3.amazonaws.com/i/3l2vn0vg40x4402vo6lm.jpg)

Now we have our log in forum.

![32-log-in-form](https://dev-to-uploads.s3.amazonaws.com/i/6inq8s5leaez9azgz3fa.jpg)

You should have received an email to accept the invitation from Netlify.

![33-you've-been-invited-to-join](https://dev-to-uploads.s3.amazonaws.com/i/7dee7ylzvx3x8h5lygrl.jpg)

If we follow the link to accept the invite we'll be taken to our live website and there will be an invite token in the URL.

![34-deployed-site-invite-token](https://dev-to-uploads.s3.amazonaws.com/i/4ml9xjya2j25wew3qbkg.jpg)

Grab the `invite_token` starting with the `#` and copy-paste it over to your localhost.

![35-localhost-invite-token](https://dev-to-uploads.s3.amazonaws.com/i/41pihd1ctwrmfspl763w.jpg)

You should now get a form to enter your password and complete your signup.

![36-complete-your-signup](https://dev-to-uploads.s3.amazonaws.com/i/1m84bslmfeyi3wm5tsgm.jpg)

If you did everything correctly then you should see your blog posts again.

![38-protected-posts](https://dev-to-uploads.s3.amazonaws.com/i/cndoe6k1jv2m2s1kfad4.jpg)

Now we want to add a link to our home page that we can use to log in and log out. We'll destructure two addition objects, `isAuthenticated` and `logOut`.

![39-isAuthenticated-logOut-destructuring-useAuth()](https://dev-to-uploads.s3.amazonaws.com/i/9jh5htvnio0ni9albagz.jpg)

We'll add another list them that uses a ternary operator to check whether we are authenticated and to display either Log Out or Log In depending on whether we are logged in or not.

![40-onClick-logIn](https://dev-to-uploads.s3.amazonaws.com/i/7q3xlfrq409dg84mftkq.jpg)

Go back to your browser and since we are logged in you should see a link for Log Out.

![41-home-page-log-out](https://dev-to-uploads.s3.amazonaws.com/i/60ti579d6q9g04n8hj71.jpg)

Now lets also add a ternary operator to the link itself so it knows to log out with we are currently logged in, and log in if we aren't currently logged in.

![42-onClick-isAuthenticated](https://dev-to-uploads.s3.amazonaws.com/i/z1o9pjd515d1ty4mpclo.jpg)

If we click Log Out the page will refresh and the link will change to Log In.

![43-home-page-log-in-link](https://dev-to-uploads.s3.amazonaws.com/i/f6ye0seq296fp5zj0sfr.jpg)

If we click Log In then we see our log in form again.

![44-log-in-form](https://dev-to-uploads.s3.amazonaws.com/i/cew9gsrpyjtoe0q4hamc.jpg)

If we log in then the link will change back to Log Out.

![45-home-page-log-out-link](https://dev-to-uploads.s3.amazonaws.com/i/1uev1vu8zzpvybqdjxds.jpg)

We'll destructure one more object called `currentUser`.

![46-currentUser-destructuring-useAuth()](https://dev-to-uploads.s3.amazonaws.com/i/3kkefgm3i8iwi3w2cnke.jpg)

We'll check to make sure we're authenticated and if so we'll show the current user's email with `currentUser.email`.

![47-isAuthenticated-logged-in-as-currentUser.email](https://dev-to-uploads.s3.amazonaws.com/i/v12fwzv6it6bm334urnk.jpg)

If we now look back in our browser you should see a message saying you are logged in.

![48-logged-in-as](https://dev-to-uploads.s3.amazonaws.com/i/0ydtnd7zzque5wvn2ryy.jpg)

And that's it! Right now you should either be feeling a great sense of accomplishment over building some amazing, or a horrible sinking feeling that you just wasted hours of your life building something useless. The choice is yours!