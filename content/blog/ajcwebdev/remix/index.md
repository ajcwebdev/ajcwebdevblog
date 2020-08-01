---
title: remix
date: "2020-06-13"
description: convention-over-configuration web application framework for react
---

![remix-logo](https://cdn.substack.com/image/fetch/w_1456,c_limit,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fbucketeer-e05bbc84-baa3-437e-9518-adb32be77984.s3.amazonaws.com%2Fpublic%2Fimages%2F4fc919c8-4d12-44f6-b4e6-807921ed65de_1312x372.jpeg)

>*The kinds of products Michael and I have built in our careers have highly dynamic data that can't be captured at build time, so we want to build a framework specifically for them (and us).*
>
>***Michael Jackson, Ryan Florence***

Remix is a web application framework for React. It's created by the developers of React Router, Michael Jackson and Ryan Florence. It aims to be a full featured convention-over-configuration solution with server rendering, data loading, and routing.

## File System Routes

![Image](https://sedaily-topics.s3.amazonaws.com/topic_images/0_2967394305479438.jpg)

Creating a new route in Remix simply requires adding a file to the "routes/" folder. Since the framework is built on React Router, layout and URL nesting can be coupled. Whenever a route nests inside another, the layouts also next.

![Image](https://sedaily-topics.s3.amazonaws.com/topic_images/0_3602088107382473.jpg)

## Suspense

Before a page renders you want to fetch the data. In the first version of React Router there was a static method on Route components called getInitialData, and some code to fetch all of it before the page rendered. This was based on Ember's "model" hook.

In React Router v1-v3 `<Route onEnter/>` got called when the route was about to be rendered. This lead to problems handling error states, providing loading UI feedback, and handling data mutations for that page.

Suspense provides APIs for loading data on route transitions without these hacks. Suspense is what motivated Ryan Florence to build Remix and he had been discussing these ideas with Michael Florence for years.


## Pricing

>*Michael and I have done a lot of open source and we absolutely love it. The core of Remix is React Router, which is free and always will be. Remix, however, is going to be a paid product. We want to put everything we’ve got into this and support the web development community with great software for many years to come.*
>
>***Michael Jackson, Ryan Florence***

Remix currently has two different pricing models:

#### Affordable Indie License

Perpetual license + two years of free updates for one person. They'll build the framework so the developers can focus on their project.

#### Commercial License

Perpetual license for a development team + annual subscription for updates and support.

Customers will have access to the GitHub repo to report issues, comment on API proposals, and send PRs with bugfixes.