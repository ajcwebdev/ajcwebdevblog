---
title: a short history of reactjs
date: "2020-04-11"
description: Its first few years, the initial community reaction, and the development of its core principles
---

React is a JavaScript library for building user interfaces. Jordan Walke created React in 2011 while working on internal tools for the Facebook Ads platform. It was first publicly deployed on Facebook's newsfeed. Pete Hunt learned of the framework in 2012 and began architecting Instagram as a single page web app built entirely with React and Backbone.Router. React was open sourced at JSConf in May 2013. Early adopters like Paul Seiffert and Clay Allsopp used it as a replacement for Backbone's view layer. The team began pitching React as the V in MVC, or the view layer of the model-view-controller pattern.

### JSX: JavaScript Syntax Extension

After being open sourced the majority of the attention and controversy was directed at an auxillarly part of the library, JSX. JSX is a language extension for JavaScript based on a similar extension for PHP that is internally popular at Facebook.

> XHP is a PHP extension which augments the syntax of the language to both make your front-end code easier to understand and help you avoid cross-site scripting attacks. XHP does this by making PHP understand XML document fragments, similar to what E4X does for ECMAScript (JavaScript).  
> -Marcel Laverdet, [XHP: A New Way to Write PHP (February 9, 2010)](https://www.facebook.com/notes/facebook-engineering/xhp-a-new-way-to-write-php/294003943919/)

ECMAScript for XML (E4X) was a programming language extension that added native XML support to ECMAScript, which at the time included ActionScript, JavaScript, and JScript. It aimed to provide an alternative to the standard DOM interface with a simpler syntax for accessing XML documents.

![JSX](https://sedaily-topics.s3.amazonaws.com/topic_images/0_8967121357493488)
[Source](https://miro.medium.com/max/3908/1*_gXwacfA-wFIW-F65J7eAw.png)

This was controversial because mixing program logic with presentation code was considered a violation of separation of concerns. For example, the Handlebar's documentation included the following quote:

> Handlebars.js and Mustache are both logicless templating languages that keep the view and the code separated like we all know they should be.

### Composable Components

Members of the core team frequently emphasized that the library did not depend on JSX. On June 5th, Pete Hunt published a blog post to explain the philosophical justification behind React called [Why did we build React?](https://reactjs.org/blog/2013/06/05/why-react.html) He emphasized the composable nature of React components.

> React is a library for building composable user interfaces. It encourages the creation of reusable UI components which present data that changes over time. Traditionally, web application UIs are built using templates or HTML directives. These templates dictate the full set of abstractions that you are allowed to use to build your UI. React approaches building user interfaces differently by breaking them into components.  
> -Pete Hunt, [Why did we build React? (June 5, 2013)](https://reactjs.org/blog/2013/06/05/why-react.html)

![Function component](https://sedaily-topics.s3.amazonaws.com/topic_images/0_3784954379404779)

### Flux: One-way data binding

Another key architectual decision of React was its emphasis on one-way data binding instead of two-way binding used in frameworks like AngularJS and Knockout.

> React was born out of frustrations with the common pattern of writing two-way data bindings in complex MVC apps. React is an implementation of one-way data bindings. "One-way data binding" foregoes the wiring of model properties to DOM manipulation for something which sounds like a really bad idea: Every time anything on our model changes, throw away the entire UI and re-render it from scratch.  
> -Lee Byron, [Quora Answer (June 7, 2013)](https://www.quora.com/How-is-Facebooks-React-JavaScript-library-How-does-it-compare-with-other-popular-JavaScript-libraries/answer/Lee-Byron)

To fully achieve this React needed something to approximate the model in an MVC architecture. This lead to the creation of Flux and a reimaging of the entire MVC architecture.

> Flux works well for us because the single directional data flow makes it easy to understand and modify an application as it becomes more complicated. We found that two-way data bindings lead to cascading updates, where changing one data model led to another data model updating, making it very difficult to predict what would change as the result of a single user interaction.  
> -Jing Chen, Bill Fisher, [Flux: An Application Architecture for React (May 6, 2014)](https://reactjs.org/blog/2014/05/06/flux.html)

Aside from blog posts and presentations explaining Flux, Facebook did not actually open source the code for their Flux implementation. This lead to many different libraries being created with wide spread confusion among developers over the different trade offs these libraries contained. Explanations of the libraries involved complex flow diagrams like this:

![Fluxxor](https://sedaily-topics.s3.amazonaws.com/topic_images/0_841985202629173)
[Source](http://fluxxor.com/what-is-flux.html)

The community eventually gravitated around Redux, an implementation Dan Abramov created for his presentation about hot loading. It contained a mostly linear flow that resembled the Elm architecture. Redux was the premiere state management solution for many years although today the community is starting to explore alternative state management solutions.

![Redux](https://sedaily-topics.s3.amazonaws.com/topic_images/0_8331088438870871)
[Source](https://www.esri.com/arcgis-blog/products/3d-gis/3d-gis/react-redux-building-modern-web-apps-with-the-arcgis-js-api/)

### React Router, Relay, React Native: World Domination

The React ecosystem expanded dramatically throughout 2015 as the community built out sophisticated solutions for routing, data fetching, and mobile. While the core remained a lightweight library, the different pieces of the ecosystem when combined started to resemble a larger full featured framework like Ember. These topics are outside of the scope of this introduction. Today React is the dominant front end framework for JavaScript where it is deployed by numerous tech companies including Airbnb, Uber, Netflix, Pinterest, and Twitter.