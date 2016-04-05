---
layout: default
---

## My musings on software design

### Embracing event driven asynchronous architecture - first steps towards micro services

As you prepare to “platformize” your product and eventually open it up to large volumes of traffic generated from both inside and outside your organization, it is important to break your product down into cohesive, yet loosely coupled components that use event driven asynchronous architectures to communicate with each other. The monolithic architecture has served you well so far. But to achieve the next level of agility and scale, both in terms of delivery, technology and business, you need to split up our application into smaller services. [Read more...](/posts/embracing-event-driven-asynchronous-architecture-first-steps-to-microservices)

### UI as a state machine

User Interfaces are all about state. Each change in UI is effectively a state transition. Thinking of UI in these terms helps us model the interactions between components as state transitions. An event occurs that changes the state of a component - there is a cause and there is an effect. Ask any UI engineer and they'll tell you that the chunk of complexity resides in component interactions, not in the components themselves. Looking at UIs from this perspective will help us appreciate why React has become so popular and how frameworks like redux and cyclejs aim to tackle this sort of complexity. [Read more...](/posts/ui-as-state-machine)

### The importance of replicable environments



### The product triangle - engineering, product, delivery

Engineering - the actual code  
Product - your user stories  
Delivery - how often you ship  
Three sides of an equilateral triangle, focus on one and ignore the other - your product will take a hit. How do you effectively manage this triangle? What are the tradeoffs that you make in a project? [Read more...](/posts/the-product-triangle-engineering-product-delivery)

### Migrating a monolithic application to a microservices architecture - things to consider
So you have decided that your application needs to be migrated to a microservices architecture. Now you need to decide where to begin, what are the things that I need to consider upfront? My current organization's customer is at a similar stage with their product. I have been working on the product for about an year now and I reckon these are some of the issues that need to be addressed before starting the journey.

* How do I go about breaking up the monolith into loosely coupled services?
* What is the best way for these services to interact with each other?
* What about security?  
* What about the development processes?
* How do I troubleshoot if something goes wrong?
* [Read more...](/posts/migrating-monolith-to-microservices)

### Business logic as state mutation
The intention of writing this post was to let out my frustration and rant about it online. About having to deal with code that makes me want to rage quit. But then I figured that would help no one. Figured I'd write a decent post and try to explain to the customer what exactly the problem with their code was and hopefully get them to agree for a refactoring. [Read more...](/posts/business-logic-as-state-mutation)

* Event Sourcing - beginning a CQRS journey
* What does it take to be agile? Stuff they don't tell you in books and blogs.
* An opinionated view on how to build angular SPAs
* What's all the fuss around "reactive"?
