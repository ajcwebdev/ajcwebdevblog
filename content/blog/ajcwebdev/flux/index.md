---
title: flux
date: "2020-05-16"
description: one way data flow
---

*Flux and React are both all about keeping a simple mental model.  
-Jing Chen (July 25, 2014)*

Flux is an application architecture that Facebook uses for building client-side web applications. It complements React's composable view components by utilizing a unidirectional data flow. It is not a framework or a library, but a design pattern inspired by CQRS. It was first debuted at F8 in May 2014 by Jing Chen, Pete Hunt, and Tom Occhino. Jing Chen started her presentation by describing issues cause by scaling an MVC application.

*MVC works pretty well for small applications. Everything has its own particular role to play. The problem is that it doesn't make room for new features. Let's look at what happens when we add a lot of models and we add a lot of views to the system. There's just an explosion of arrows.  
-Jing Chen, [Hacker Way: Rethinking Web App Development at Facebook (May 4, 2014)](https://www.youtube.com/watch?v=nYkdrAPrdcw)*

![Image](https://sedaily-topics.s3.amazonaws.com/topic_images/0_8200405328446236)

She described a recurring bug in the Facebook Chat system. Users would frequently see a red number over their chat icon signifying an unread message, but when they clicked the icon there would not be any new messages. Facebook's engineers would think that they fixed the bug but it would continually reappear due to the fragility of the coupled architecture. Some engineers referred to this as the "Banana vs. Jungle" problem: you ask for a banana but instead you get back a banana, a gorilla holding the banana, and a jungle containing the gorilla. The Facebook engineers had discovered the need for command-query separation.

*We found that two-way data bindings lead to cascading updates, where changing one data model led to another data model updating, making it very difficult to predict what would change as the result of a single user interaction.
-Bill Fisher, Jing Chen, [Flux: An Application Architecture for React (May 6, 2014)](https://reactjs.org/blog/2014/05/06/flux.html)*

### Command Query Responsibility Segregation

Command–query separation is a principle stating that every method should either be a *command* that performs an action, or a *query* that returns data to the caller, but not both. In other words, asking a question should not change the answer. Command query responsibility segregation (CQRS) applies the CQS principle by using separate Query and Command objects to retrieve and modify data, respectively. CQRS fits well with event-based programming models, see [Javascript Topic Page](https://www.softwaredaily.com/topic/javascript) for a description of how JavaScript handles events in the browser.

## Dispatcher, Store, Views

Flux eschews MVC in favor of a unidirectional data flow as described on the [React Topic Page](https://www.softwaredaily.com/topic/reactjs). When interacting with a **view (React component)** an action is propagated through a central **dispatcher** to **stores** that hold the application's data and business logic. The stores then update all affected views. The stores accept updates and reconcile them as appropriate, rather than depending on something external to update its data in a consistent way. Nothing outside the store has insight into how it manages data for its domain and there are no direct setter methods.

The flux documentation suggests the following diagram should be the primary mental model for Flux. The dispatcher, stores and views are independent nodes with distinct inputs and outputs. Actions are simple objects containing new data and an identifying type property:

![Unidirectional data flow diagram (Action -> Dispatcher -> Store -> View)](https://facebook.github.io/flux/img/overview/flux-simple-f8-diagram-1300w.png)
*Data in a Flux application flows in a single direction.  
-[Flux Documentation](https://facebook.github.io/flux/docs/in-depth-overview/)*

The views may cause a new action to be propagated through the system in response to user interactions:

![Flux diagram of client action](https://sedaily-topics.s3.amazonaws.com/topic_images/0_1861436422799183)

## Redux

Redux is a predictable state container for JavaScript apps. It aims to help applications behave consistently and run in different environments (client, server, and native). While Redux was originally created to be used with React it can also be integrated with any other view library.

### Reducers, Actions, Store

Reducers are pure functions that take in the state and an action as parameters. The action describes how the state will change. The store is a global variable that holds all of your applications state. The store is known as the single source of truth because it is a global variable that holds all the state in the app.

Redux was created by Dan Abramov for a presentation he gave about hot loading. Redux was a secondary concern for him, but his succinct explanation led to many adopting his version of the Flux architecture.

*Stores are stateful. If you re-execute the store code it's going to get the new initial state. The state is lost, the subscriptions are lost, it's a bummer. But it doesn't have to be this way. As I was thinking more about trying to work around this and to fit Flux into React hot loader workflow I figured out that store in Flux does too many things. It has too much boilerplate. And I'm not talking about the switch statements. The real boilerplate is in concepts, not in syntax.  
-Dan Abramov, [Live React: Hot Reloading with Time Travel (July 5, 2015)](https://www.youtube.com/watch?v=xsSnOQynTHs)*

Since then Redux has been the dominant state management solution for React application. But in a series of SEDaily interviews with React luminaries, many expressed a need to move beyond Redux. Other options such as MobX and the Context API have started to be used as substitutes for Redux as state management for React applications.

![Image](https://sedaily-topics.s3.amazonaws.com/topic_images/0_4744775498652225.jpg)