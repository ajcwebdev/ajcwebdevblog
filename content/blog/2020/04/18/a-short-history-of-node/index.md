---
title: node
date: "2020-04-18"
description: node, npm, and the ecosystem of libraries they enabled
---

Node.js is a JavaScript runtime environment for executing JavaScript code on a server instead of a web browser. It was created in 2009 by Ryan Dahl out of his frustration with Apache Server's inability to scale concurrent connections into the hundreds of thousands. Many attempts at putting JavaScript on the server had been attempted, starting in the mid-90s with Netscape's LiveWire Pro Web. Node's power and success comes from two key features, it is *event driven* with *asynchronous input-output*.

**Event Driven**: A programming paradigm in which the flow of the program is determined by events such as user actions (mouse clicks, key presses), sensor outputs, or messages from other programs or threads.
**Asynchronous I/O**: A form of input/output processing that permits other processing to continue before the transmission has finished.

[![Image](https://sedaily-topics.s3.amazonaws.com/topic_images/0_4129993339286535.jpg)](https://twitter.com/imneutralchaos/status/494959181871316992)

*The thesis is that IO has to be done differently. We're doing it wrong... everything... the way that we're thinking about doing IO really makes things difficult. Writing servers and writing any soft of application is difficult because of how we're doing IO.
-Ryan Dahl, [node.js (November 8, 2009)](https://www.youtube.com/watch?v=ztspvPYybIY)*

### V8

Node builds on top of Google's V8 Javascript engine with the addition of an event loop and non-blocking IO. V8 compiles JavaScript directly to native machine code using just-in-time compilation. It's important to emphasize that Node and V8 are not written in JavaScript, they are runtime environments written in C/C++ that execute JavaScript code.

![Image](https://sedaily-topics.s3.amazonaws.com/topic_images/0_45149077309280927)

### Socket.io

A popular early use case for Node was to build websocket servers like a chat server. Lots of browser connect to the server and messages are sent back and forth between the client and the server while the socket stays open. In 2010 Guillermo Rauch built socket.io, a framework for this specific use case.

![Image](https://sedaily-topics.s3.amazonaws.com/topic_images/0_27532092743435954)

### Joyent

After giving the inaugural presentation for Node, Ryan Dahl was approached by Mark Mayo from Joyent. They were also working on server side JavaScript and wanted to hire Ryan Dahl to [build out Node while working as a Joyent employee](https://www.youtube.com/watch?v=L_JKb61EalQ). Bryan Cantrill described Node as being to [Joyent what Java was to Sun](http://dtrace.org/blogs/bmc/2010/07/30/hello-joyent/). For some reason he seemed to think this was a positive comparison.

![Image](https://sedaily-topics.s3.amazonaws.com/topic_images/0_1017477370946176)

In January 2012, Dahl believed that the Node project was "done," and stepped aside. He promoted Isaac Schlueter to manage the project and also sold the intellectual property of Node to Joyent. After two years Schlueter believed the greatest opportunity for Node was in the growing ecosystem of packages and modules. He passed the Node project along to Timothy J. Fontaine so he could focus on npm inc. Unlike Dahl, Schlueter maintained legal ownership of his intellectual property.

### npm

Node's rise to prominence was helped by its tight integration with npm, a package manager created by Isaac Schlueter that made it incredibly easy for programmers to publish modules. This allowed easy code sharing and enabled a Cambrian explosion of JavaScript programs.

*I think node needs a package manager.  There are a lot of very useful modules out there, but it's tricky right now to actually use more than one of them together. Here's a proposal for a very lightweight and simple way to alleviate the situation.  I'm calling it npm, and it should be able to install itself fairly soon. :)
-Isaac Schlueter, [Preview: npm, the node package manager (September 30, 2009)](https://groups.google.com/forum/?hl=en#!topic/nodejs/erDWyS4xPw8)*

Npm was owned and maintained by a private company, npm inc, for most of Node's lifetime. This lead to friction with the open source community and in 2019 former CTO of npm inc, C J Silverio, [announced a competing package manager](https://www.youtube.com/watch?v=MO8hZlgK5zc) to address concerns about centralized ownership of the package registry.

*Success is a catastrophe for a lot of projects. It's a catastrophe that you need to survive and success for npm was a catastrophe, here's why. Npm's package registry is centralized. It's not just a CLI tool that grabs the code and puts it on your hard drive. The CLI is probably the least important part of the npm machinery despite how frequently you interact with it. Npm is most importantly a centralized package registry and repository.
-C J Silverio, [The Economics of Open Source (June 3, 2019)](https://www.youtube.com/watch?v=MO8hZlgK5zc)*

In contrast, Ryan Dahl in a retrospective talk about Node claimed "npm (AKA "Isaac") decoupled the core Node library and allowed the ecosystem to be distributed."

![Image](https://sedaily-topics.s3.amazonaws.com/topic_images/0_16581183117663367)

Npm inc was acquired by GitHub in March 2020 (GitHub itself was acquired by Microsoft in 2018). The jury is still out whether this is better or worse.

### io.js
 
On Thanksgiving Day in 2014, Fedor Indutny started io.js, a fork of Node.js. Other members of the team described it as a "table flipping moment" for Fedor, who was frustrated by the length of time required for Joyent to approve his pull requests. Even though the fork was sparked by a single individual over a seemingly singular issue, it became a rallying cry for many in the community who saw larger systemic issues.

Node was not staying up-to-date with the latest releases of the Google V8 JavaScript engine and lacked support for new features in ES2015. The community was dissatisfied with Joyent's stewardship of the project and io.js was created as an open governance alternative with a separate technical committee.

![Image](https://sedaily-topics.s3.amazonaws.com/topic_images/0_24258206719389475)

In February 2015, the intent to form a neutral Node.js Foundation was announced. By June 2015, the Node.js and io.js communities voted to work together under the Node.js Foundation. In September 2015, Node.js v0.12 and io.js v3.3 were merged back together into Node v4.0. This merge brought V8 ES6 features into Node.js and a long-term support release cycle.

*The Node.js and io.js developer communities today are announcing a collaboration to merge their respective code bases and continue their work in a neutral forum, the Node.js Foundation, hosted by The Linux Foundation.
 -[Node.js Foundation Advances Community Collaboration, Announces New Members and Ratified Technical Governance (June 15, 2015](https://www.linuxfoundation.org/press-release/2015/06/node-js-foundation-advances-community-collaboration-announces-new-members-and-ratified-technical-governance/))*

 
### Node Today

In a JS Party interview on April 2, 2020, Guillermo Rauch lamented the failure of Node to go further as an industry trend, believing that it would have been much bigger and have more enterprise success. Even the creator of Node believes that we need to move beyond it. Dahl gave a talk called "10 Things I Regret About Node.js" at JS Conf in 2018 which also annouced a Node competitor called Deno which aims to address Node's shortcomings in security, project building, and modules. Deno 1.0 was released on May 13, 2020.

Despite these criticisms Node continues to be one of the most popular choices for bootcamps and online tutorials teaching the principles of full stack development. The advantages of building your front end and your back end in the same language has proved to be a force multiplier, especially for new programmers trained only in JavaScript. Companies deploying Node today include Netflix, PayPal, Trello, Capital One, LinkedIn, Yahoo, Mozilla, Uber, Groupon, Ebay, and Walmart.