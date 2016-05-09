---
layout: page
---

### Microservices: Splitting data up at the physical layer.
In the previous article, [Microservices: Splitting up your domain models](/#), we have walked through the concepts of an aggregate root and boundaries and how these concepts can help us take that first step in splitting up our monolith into multiple microservices. The issue of splitting up our application data along the aggregate boundaries at the physical layer (i.e. databases) still remains. If you haven't already read the previous article, I suggest you do - it gives the right context to what follows.

Continuing with the previous article's example of the Survey aggregate root, we have concluded that it is better if the aggregate boundary is explicit. That the Survey aggregate root should not contain the Project and Customer aggregate roots directly, but hold references to them via simple Id fields - 'projectId' and 'customerId'.

Clearly, the aggregate root is now treating 'Project' and 'Customer' entities as external to its own system and it knows that it can retrieve them as long as it has their ids. When we are handling (as in processing this entity to perform some fancy business logic) the 'Survey' aggregate root, should there be a need to retrieve the corresponding 'Project' or 'Customer', all we need to do is call the right api method on the microservice with the right projectId. For all we care, the 'Project' entity corresponding to that 'projectId' can be from a relational database, from a document database or even an external service. The 'Survey' aggregate root doesn't and shouldn't care about how the 'Project' entity is stored physically, so long as it has knowledge of which service to invoke to get the 'Project' entity.

// Insert diagram explaining the above paragraph.

Alright, so you get the point. Aggregate roots outside of their own systems can be referenced by their Ids. But do we really want to share the database primary key with an outside system? So your primary key

Remember, your application is probably not at this stage yet. For your application to get there, you will have to first make changes to your domain models and then generate explicit Ids
