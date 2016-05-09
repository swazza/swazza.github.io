---
layout: default
---

## My opinionated musings on software design

### Embracing event driven asynchronous architecture - first steps towards micro services
As you prepare to “platformize” your product and eventually open it up to large volumes of traffic generated from both inside and outside your organization, it is important to break your product down into cohesive, yet loosely coupled components that use event driven asynchronous architectures to communicate with each other. The monolithic architecture has served you well so far. But to achieve the next level of agility and scale, both in terms of delivery, technology and business, you need to split up our application into smaller services. [Read more...](/posts/embracing-event-driven-asynchronous-architecture-first-steps-to-microservices)

### UI as a state machine
User Interfaces are all about state. Each change in UI is effectively a state transition. Thinking of UI in these terms helps us model the interactions between components as state transitions. An event occurs that changes the state of a component - there is a cause and there is an effect. Ask any UI engineer and they'll tell you that the chunk of complexity resides in component interactions, not in the components themselves. Looking at UIs from this perspective will help us appreciate why React has become so popular and how frameworks like redux and cyclejs aim to tackle this sort of complexity. [Read more...](/posts/ui-as-state-machine)

### The importance of replicable environments
Let's start out by understanding what an 'environment' is. Let's keep it simple - I'd like to call the 'world' in which your application's code executes as it's environment. This 'world' can be made up of hardware (CPUs, Memory, Network Components, Storage), software (OS, Databases, Managed Runtimes), data and even configuration. For a simple Hello, World! program written in Java, the environment would be the JVM itself and the box on which it runs, including the OS and the underlying hardware. But for software of any value, it's environment composition will likely be significantly more complex. This article takes a look at why it is important to be able to create consistent and replicable environments on demand for your business app and explores some of the practices and tools available to that end. [Read more...](/posts/replicable-environments)


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

### Microservices: Splitting data up at the physical layer.
In the previous article, [Microservices: Splitting up your domain models](/#), we have walked through the concepts of an aggregate root and boundaries and how these concepts can help us take that first step in splitting up our monolith into multiple microservices. The issue of splitting up our application data along the aggregate boundaries at the physical layer (i.e. databases) still remains. If you haven't already read the previous article, I suggest you do - it gives the right context to what follows. [Read more...](/posts/microservices-splitting-data-at-physical-layer)

### Microservices: Where do I put my business logic?
Now that you have split up the domain models and data, the next obvious question would be where does all the business logic go? [Read more...](/posts/microservices-business-logic)

### Business logic as state mutation
The intention of writing this post was to let out my frustration and rant about it online. About having to deal with code that makes me want to rage quit. But then I figured that would help no one. Figured I'd write a decent post and try to explain to the customer what exactly the problem with their code was and hopefully get them to agree for a refactoring. [Read more...](/posts/business-logic-as-state-mutation)

### Apr 2016, NYC - O'Reilly Software Architecture Conference
I was fortunate enough to attend the O'Reilly Software Architecture Conference, 2016 held in NYC. As if attending the conference wasn't good enough, I also had the fortune of attending as a platinum pass member. This gave me access to a two day workshop followed by two days of access to a bunch of keynotes on microservices, reactive systems and some other topics that Enterprises are beginning to adopt at a wide scale. I choose to attend the two day workshop on 'Designing for Volatality' by [Allen Holub](https://www.linkedin.com/in/allenholub). Now before you continue to read on, I'd like to mention that what follows is MY interpretation of what Allen mentioned in the workshop. It is quite possible that what Allen intended for us to interpret and what I did end up interpreting might be completely different. But I'd like to think my interpretation is close to accurate :). [Read more...](/posts/orielly-sa-conf-2016).

* Event Sourcing - beginning a CQRS journey
* What does it take to be agile? Stuff they don't tell you in books and blogs.
* An opinionated view on how to build angular SPAs
* What's all the fuss around "reactive"?
