---
title: "How getters and setters harm encapsulation"
date: "2018-12-09"
tags: [object oriented design,encapsulation]
image: img/posts/encapsulation.jpg
---

Taking a step back and looking at something that you've been doing for years with a *fresh* perspective can lead to profound insights. I had an insight exactly like this a few months ago, when I decided to look at `getters` and `setters` from a different point of view.

During my first steps as a software engineer, I learned about Plain Old Objects (POJOs for Java software engineers, like myself) and ever since it made sense in my head, I always took `getters` and `setters` for granted. It was something I *had* to do. Later on, I learned (although now I know that I did not fully understand at the time) about the notion of encapsulation and how these `getters` and `setters` are a key step to achieving it. It then made even more sense to *always* code (or rather generate) them in every single POJO in my code.

So I did consistently, until I read a blog post that got me thinking and revisiting the whole concept of encapsulation in a fresh, unbiased way. Now, that I believe the dust has settled, I will try to communicate my thoughts on the matter in this post.

# Object-oriented design

It all starts with true object-oriented design. If one goes online looking for a definition and a brief description of Object-Oriented Programming (OOP), one will come across (among some wise stuff) all kinds of nonsense. They usually start with something like *"OOP is about modeling the real world..."*. Well, it's not.

OOP is a design *philosophy* according to which, a software system should consist of a set of *self sustainable* objects and *messages* that can be passed between these objects. Now, notice that the two key words here are *self sustainable* and *messages*. In other words, our objects should be:

* empowered to accomplish what lies within their responsibility (which had better be a single one) and
* their outside world (other objects) should have a way of telling them what they need them to do

This is really straightforward. Let's assume that we have an `AirCondition` object. What we would like is to be able to **tell** it to adjust the room temperature to (say) 25 degrees Celsius and for it to be able to do so. Notice that we are not interested in *how* is it going to achieve this. All we want is to *command* it and have the job done. Essentially, we are *sending a message*. We are *delegating* the task. Now, this brings us to the point that we can understand both what encapsulation is and why we need it.

# Encapsulation

The gist behind the notion of encapsulation is that the *objects should not reveal their internals* (implementation details) *to the outside world* (other objects). They should be like black boxes, providing an interface for the world, allowing it to tell them what needs to be done. All the details of *how* they achieve the tasks that are *told* to achieve it's *their* business and no one else's.

In a technical level, an object exposes a set of public methods (API) and probably uses variables and data structures to manage it's state in order to perform the tasks that it's told to perform.

> Encapsulation mandates that the state of the object should be kept private, unknown to the external world, at any given time.

# The problem with `getters` and `setters`

This is exactly where `getters` and `setters` enter the picture. Conventional wisdom has it that since the object's properties are to remain "hidden", they should be wrapped by a `getter` and `setter` each, enabling the external world to "access" them, without learning about the object's state. Now, pause for a minute and read this last sentence once again before proceeding. *Does it make any sense at all?* At the end of the day, what difference does it make if we are to use the properties either directly or via their wrapper `getter` and `setter`? Essentially we are messing with the object's state in either case - which is quite overtly exposed to the public via these methods.

# An example

In order to better illustrate the nature of this problem, let's consider for a moment the `AirCondition` class from above. Suppose our intention was to adjust the room temperature to 25 degrees Celsius. One could achieve this via the following piece of code:

```
if (airCondition.getTemperature() > 25) {
  while (airCondition.getTemperature() > 25) {
    airCondition.decrementTemperature();
  }
} else if (airCondition.getTemperature() < 25) {
  while (airCondition.getTemperature() < 25) {
    airCondition.incrementTemperature();
  }
}
```

However, all we do is constantly manipulating the object's state, essentially **implementing the logic that it should possess**. We are *micromanaging* the object. Instead, we should *trust* it on knowing how to do its job. We keep on **asking** about it's state and then modify it instead of **telling** it the end result that we wish. Conforming to OOP, all we need to do is to *send it a message*, like the following

```
airCondition.adjustTemperatureTo(25)
```

and it should get the job done, because it *knows* how to actually do it. We shouldn't even know if there is or there is not a property holding the current temperature, let alone query for it directly. This is part of the means the `AirCondition` class could use to achieve its purposes, it's subject to change at any given moment and its strictly **its own business**.

# Tight coupling

We all know (at least in principle) that our classes should be *highly cohesive* and *loosely coupled*. The theory is great, but let's consider how these guidelines (about coupling in particular) apply to this specific example.

Let's assume that we wish to refactor the `AirCondition` class. Perhaps we would like to rename the `temperature` variable to `currentTemperature`. Performing this elementary refactoring move, would create a chain reaction, causing all the classes that depend upon it (its collaborators) to fail to compile and impose the need to refactor them too. Perhaps, some collaborators of these collaborators should be refactored as well and so forth.

This scenario illustrates perfectly the side effects of a design with tightly coupled classes. However, on the second, *imperative* approach, the collaborators of the refactored, `AirCondition` class would remain unaffected, agnostic to the modification. We can therefore conclude that *the imperative approach has led to a more loosely coupled design*.

# Tell, don't ask

Some of you might have already noticed that these ideas start to sound a lot like the *Tell, don't ask* principle (also known as *Law of Demeter*). (In case you're not familiar with this principle, feel free to look it up online as I will not delve into its details in this post). The essence behind the principle, which is in total accordance with the previously expressed ideas is that objects are not to be treated as data structures. Splitting the data and the operations on these data in different objects is not wise.

> Data and functionality that depends on these data belong in the same object

# A story and a lesson learned

Once, while working for a company heavily based on microservices, I had to implement a small feature in a microservice I wasn't normally contributing to. While studying the code I quickly realized that it was a common practice to access class properties directly. I actually ended up walking into a tech leads meeting trying to explain both what encapsulation is and why it would be beneficial to use it, by wrapping properties with `getters` and `setters`.

Eventually, I failed to pass the message (at least adequately enough to initiate a change), which made me sad, but what made me even sadder was the realization, later in my life, that even if I had convinced this group of people to start using `getters` and `setters` instead of directly accessing the properties, essentially not a thing would have been changed in terms of the quality of the code and the product.

At the end of the day, what difference would it make to use `airCondition.getTemperature()` instead of `airCondition.temperature`? Perhaps that is the reason why the designers of Kotlin decided to provide `getters` and `setters` by default, without even going into the trouble to code (generate) them or even call(!) them (in Kotlin `airCondition.temperature` actually calls `airCondition.getTemperature()` under the hood).

# Amending the situation

Assuming that the problem is clear, a reasonable question to ask would be what to do to amend it. A very helpful first step would be to stop writing `getters` and `setters` this very moment. This would surface cases that collaborators need access to another classe's properties.

When you face such a situation, take a moment and reflect. *Do you really need to expose this property*? Is there a better way to solve the problem? Perhaps, instead of exposing the property, a new method can be introduced in the object to receive the message that an operation needs to be performed. Exactly the operation that the collaborator who wanted access on the property was about to implement. *Whose responsibility is this operation*?

Sometimes `getters` and `setters` will be needed, but I reckon that most of the times, different, better object-oriented solution will present themselves. This will gradually improve the design of the system you are working on.

# Conclusion

Object-oriented design is all about passing messages between self sustainable objects and ecapsulation is a tool that can be immensely helpful on this task by resulting in loose coupling. On the other hand, letting our classes see deeply into the internal implementation of their collaborators, essentially results in tight coupling.

Wrapping class properties with `getters` and `setters` helps look deep inside the internals of other class. It provides a **false** sense of encapsulation, but even worse, it pushes us towards treating classes as mere data structures and implementing the logic that these data serve in collaborators, defeating the very purpose of true object-oriented design.

Experiment by stop writing `getters` and `setters` instead and observe the side effects. I strongly believe that it will lead to a better design.
