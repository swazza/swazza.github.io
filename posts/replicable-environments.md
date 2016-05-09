---
layout: page
---
### The importance of replicable environments
Let's start out by understanding what an 'environment' is. Let's keep it simple - I'd like to call the 'world' in which your application's code executes as it's environment. This 'world' can be made up of hardware (CPUs, Memory, Network Components, Storage), software (OS, Databases, Managed Runtimes), data and even configuration. For a simple Hello, World! program written in Java, the environment would be the JVM itself and the box on which it runs, including the OS and the underlying hardware. But for software of any value, it's environment composition will likely be significantly more complex. This article takes a look at why it is important to be able to create consistent and replicable environments on demand for your business app and explores some of the practices and tools available to that end.

Typically, your application will be multi tiered with your business logic distributed across multiple web front ends, your data replicated over multiple database servers and you will have cross cutting concerns like logging, caching, identity management, etc all running in their own sub systems. This is a complex environment - an environment

It is not uncommon for enterprises to have multiple environments through which the apps have to go 'graduate' through before a new version is released to production. Ask any QA or Developer who have worked in such setups and they will tell you about the bugs resulting due to inconsistencies across environments. Your typical setup would include a 'Developer Integration' (Dev-Int) environment, a QA environment, a Staging/UAT environment and then finally the Production environment. How often have your developers and QAs argued about 
