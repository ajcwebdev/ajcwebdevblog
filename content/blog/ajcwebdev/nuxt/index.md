---
title: nuxt
date: "2020-09-04"
description: intuitive vue framework for creating modern web applications
---

NuxtJS is an intuitive Vue framework created by [Sébastien Chopin in October 2016](https://github.com/nuxt/nuxt.js/commit/0072ed31da6ce39d21046e05898f956cff190390). It is a progressive framework designed for creating modern web applications. It is based on official Vue libraries including Vue Core, Vue Router, and Vuex.

It was inspired by NextJS and much like that React framework it started as a solution for server-side rendering. In recent years though it has expanded to include [static site generation](https://nuxtjs.org/blog/nuxt-static-improvements/) inspired by projects like Gatsby and Gridsome.

Nuxt.js automatically generates the vue-router configuration based on your file tree of Vue files inside the pages directory. When you create a .vue file in your pages directory you will have basic routing working with no extra configuration needed.

To start we will enter the following commands:
1. `mkdir ajcwebdev-nuxt` to create a directory
2. `cd ajcwebdev-nuxt` to change to that directory
3. `touch package.json` to create our `package.json` file
4. `code .` to open VS Code

![00-create-project](https://dev-to-uploads.s3.amazonaws.com/i/1hvv17ysr1fwko31rhbq.jpg)

Enter the following code into `package.json` to give our project a name and basic scripts.

![01-package-json](https://dev-to-uploads.s3.amazonaws.com/i/8u12kvt9f6g5ezez81n3.jpg)

To install Nuxt we will enter `yarn add nuxt`.

![02-yarn-add-nuxt](https://dev-to-uploads.s3.amazonaws.com/i/7zfqvl8eqq7qn91chklf.jpg)

This will install a butt load of dependencies. Trust the dependencies. Believe in the dependencies.

![03-dependencies](https://dev-to-uploads.s3.amazonaws.com/i/1ug0iedugcn541pzqayb.jpg)

If we check out `package.json` file we'll see `nuxt` has been installed with version `2.14.4`.

![04-package-json-nuxt](https://dev-to-uploads.s3.amazonaws.com/i/xrc7gha1hbd3heyqkin8.jpg)

To create our first page will enter the following commands:
1. `mkdir pages` to create our pages directory
2. `touch pages/index.vue` to create a file called `index.vue`

![05-mkdir-pages](https://dev-to-uploads.s3.amazonaws.com/i/5l35wqmeakrca6jk6pzb.jpg)

Open `index.vue` and enter the following Vue code.

![06-index.vue](https://dev-to-uploads.s3.amazonaws.com/i/oo7jn1w72ymnnmdqzf4j.jpg)

We'll use the `yarn dev` command to start our development server.

![07-yarn-dev](https://dev-to-uploads.s3.amazonaws.com/i/dsl5ecnni6hzlnqad8yq.jpg)

You'll be asked if you want to allow Nuxt to collect anonymous data about usage.

![08-data](https://dev-to-uploads.s3.amazonaws.com/i/thp2hzc3mvkd7z7fhwf2.jpg)

The answer to that question is between you and your God.

![09-dev-server](https://dev-to-uploads.s3.amazonaws.com/i/gcu62bvxguz7m8veyo2f.jpg)

Open up `localhost:3000` in a browser.

![10-hello-world](https://dev-to-uploads.s3.amazonaws.com/i/kdwlq00745dx1xceheb9.jpg)

If we open up our dev tools we can see the source.

![11-dev-tools](https://dev-to-uploads.s3.amazonaws.com/i/glmxa76quuef6twazd9f.jpg)

Here is what our current directory structure looks like.

![12-directory-structure](https://dev-to-uploads.s3.amazonaws.com/i/xe15y24zzp5yh5g4v5s0.jpg)

The `.nuxt` directory is where the magic is happening.

![13-nuxt-directory](https://dev-to-uploads.s3.amazonaws.com/i/slarecx7i09ma6plue7d.jpg)

In the next part we will explore all this code. We will also create another page and link between them.