---
title: a first look at vue 3: part 1 - setup
date: "2020-10-18"
description: install and create our first vue application
---

## What is Vue.js?

Vue (pronounced /vjuː/, like **view**) is a **progressive framework** for building user interfaces. Unlike other monolithic frameworks, Vue is designed from the ground up to be incrementally adoptable.

The core library is focused on the view layer only and is easy to integrate with other libraries or projects. Vue can also be used in combination with modern tooling to power sophisticated Single-Page Applications.

## Getting Started

First we'll install the CLI.

```bash
yarn global add @vue/cli
```

![01-yarn-add-vue-cli](https://dev-to-uploads.s3.amazonaws.com/i/wvdqwfgn9jav121sejgc.jpg)

`vue --version` will display the current version.

![02-vue-version](https://dev-to-uploads.s3.amazonaws.com/i/ya7otqbtvjsp8vokfmj8.jpg)

`vue -h` will display available commands.

![03-vue-help](https://dev-to-uploads.s3.amazonaws.com/i/qgx4alhdya4p6am2in3t.jpg)

Since ES Modules are awesome, we'll use [Vite](https://github.com/vitejs/vite) to generate our Vue project.

```bash
yarn create vite-app ajcwebdev-vue3
```

This command creates a Vite project called `ajcwebdev-vue3`. Feel free to name your project whatever you want, just make sure to use your project name anytime I use `ajcwebdev-vue3` in a terminal command.

![04-create-vite-app](https://dev-to-uploads.s3.amazonaws.com/i/5rmlld2taahi898axva6.jpg)

```bash
cd ajcwebdev-vue3
yarn
```

`cd` into the new project directory and enter `yarn` to install the dependencies.

![05-yarn-install](https://dev-to-uploads.s3.amazonaws.com/i/irke83vcmmp522kxlj68.jpg)

```bash
yarn dev
```

`yarn dev` will start our development server.

![06-yarn-dev](https://dev-to-uploads.s3.amazonaws.com/i/ywf6g81xci6lwldz1k34.jpg)

Open a browser and go to `localhost:3000` to see the default starter page.

![07-homepage](https://dev-to-uploads.s3.amazonaws.com/i/sxtv3colexsvqxs8cb25.jpg)

Click the count button to increment the number.

![08-click-count](https://dev-to-uploads.s3.amazonaws.com/i/4r3iaydosui0erwf1y0y.jpg)

Now open up the project and look at the directory structure.

![09-project-structure](https://dev-to-uploads.s3.amazonaws.com/i/5x7dq265wiqyte12yde6.jpg)

There are three folders:
* `node_modules` for all our dependencies, if you look in here it will stress you out so don't ever do that
* `public` contains the favicon icon displayed on browser tabs
* `src` project files that we will be editing

And four files:
* `.gitignore` for files we don't want to commit to git such as our `node_modules`
* `yarn.lock` to lock our dependency versions
* `package.json` for managing our scripts and dependencies
* `index.html` where the entire application is loaded into the main `div`

![10-package.json](https://dev-to-uploads.s3.amazonaws.com/i/7o5t68kdwukksa5iolxq.jpg)

We have two scripts:
* `dev` for local development
* `build` bundles the code for production

`Vue` is our only dependency along with two development dependencies: `vite` and `@vue/compiler-sfc` which is a package containing lower level utilities that you can use if you are writing a plugin/transform for a bundler or module system that compiles Vue single file components into JavaScript.

![11-index.html](https://dev-to-uploads.s3.amazonaws.com/i/dabsf0qikmwzovexchlh.jpg)

In the body we load the `main.js` file in a `script` tag. The application is loaded into the main `div` on line 10.

![12-public-src](https://dev-to-uploads.s3.amazonaws.com/i/xk48l9s43xzehoptl29q.jpg)

In our `src` folder we have three files:
* `App.vue`
* `index.css`
* `main.js`

And two folders:

* `assets`
* `components`

![13-main.js](https://dev-to-uploads.s3.amazonaws.com/i/45b2k5o345574rumtqb9.jpg)

`App` is imported and mounted with `createApp()`

![14-app.vue](https://dev-to-uploads.s3.amazonaws.com/i/xd19f3ghihd6guvlksoj.jpg)

A Vue component contains a `template` for our HTML and a `script` for our JavaScript. In the script we are importing the `HelloWorld` component and exporting the `App` component. The `HelloWorld` component is rendered in the template with a message passed in.

![15-assets-components](https://dev-to-uploads.s3.amazonaws.com/i/qdla1gq85gyy6btv0s5o.jpg)

In our components folder we have the `HelloWorld` component that is imported in `App`.

![16-HelloWorld.vue](https://dev-to-uploads.s3.amazonaws.com/i/xhfz6xobi0ybce9mv3z0.jpg)

The template contains the `msg` object we passed into `HelloWorld` back in our `App` component. It also has a button with `@click="count++"` to increment our `count` variable. `@` is a shorthand for the `v-on` directive which listens to DOM events.

![17-App.vue-edit](https://dev-to-uploads.s3.amazonaws.com/i/7ohzhgxri0o0nyb1fyfm.jpg)

To make sure everthing is working we'll make a few edits to `App` by taking out the logo and changing the `msg` object.

![18-HelloWorld.vue-edit](https://dev-to-uploads.s3.amazonaws.com/i/fgng8mae60nfsgkqxvao.jpg)

We'll also edit the `HelloWorld` component by taking out the `count` object and editing the `template`.

Save your changes and return to the browser.

![19-homepage-edit](https://dev-to-uploads.s3.amazonaws.com/i/sh69a5ttavkv4i4aa23g.jpg)

In the next part we'll learn how to create multiples pages and link between them.