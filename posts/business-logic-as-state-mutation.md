---
layout: page
---

## Business logic as state mutation
The intention of writing this post was to let out my frustration and rant about it online. About having to deal with code that makes me want to rage quit. But then I figured that would help no one. Figured I'd write a decent post and try to explain to the customer what exactly the problem with their code was and hopefully get them to agree for a refactoring.

Before we get into how the code was written in the module that we have been working on, let us go over some stuff together. For the sake of simplicity, let us agree upon the meaning of the word 'Domain' - let us think of the 'Domain' as encompassing everything in context of the problem that you are trying to solve and 'Domain Model' as the set of all classes that represent your 'Domain' <sup>1</sup>. Assuming you have some exposure to DDD, you'd want your 'Domain Models' to not be anaemic (just a property bag) but rich instead - so that they represent both the state and behavior of what they are trying to model.

Most of your business logic will

_____________________________________________________________________________________________________________________________________________
1. I'm not quoting Eric Evans or Martin Fowler for I believe I still have a way to go to make complete sense of DDD - Domain Driven Design and don't want to rake up a shit storm from DDD purists.
