---
title: "How getters and setters harm encapsulation"
date: "2018-12-08"
tags: [object oriented design,encapsulation]
image: img/posts/encapsulation.jpg
---

Taking a step back and looking at something that you've been doing for years with a new, *fresh* perspective can lead to profound insights. I had an insight like this a few months ago, when I decided to look at `getters` and `setters` from a different point of view.

During my first steps as a software engineer, I learned about the value of Plain Old Objects (POJOs for Java software engineers, like myself) and ever since it made sense in my head, I always took `getters` and `setters` for granted. It was something I *had* to do. Later on, I learned (or so I believed at the time), about the notion of encapsulation and how these `getters` and `setters` are a key ingredient to achieve it. It made even more sense then to *always* code (or rather generate) them in every single POJO in my code.

So I did consistently, until a blog post I read got me thinking and revisiting the whole concept of encapsulation in a fresh, unbiased way. Now, that I believe the dust has settled, I will try to communicate my thoughts in this post.

# The mighty OOP

If one goes online looking for a definition and a brief description of Object Oriented Programming (OOP), one will come across, among some wise words, all kinds of nonsense. They usually start with something like *"OOP is about modeling the real world..."*. Well, it's not. OOP is a design *philosophy* according to which, a software system should consist of a set of *self sustainable* objects and *messages* that can be passed between these objects. Now, notice that the two key words here are *self sustainable* and *messages*.

In other words, our objects should be:

* empowered to accomplish what lies within their responsibility (which had better be a single one) and
* their outside world (other objects) should have a way of asking them to do something

This is really straightforward. Let's assume that we have an `AirCondition` object. What we would like is to be able to **tell** it to adjust the room temperature to 25 degrees Celsius and for it to be able to do so. Notice that we are not interested in *how* is it going to achieve this. All we want is to *command* it and have the job done. Essentially, we are *sending a message*. We are *delegating* the task. Now, this brings us to the point that we can understand both what encapsulation is and why we need it.

# Encapsulation

What encapsulation is essentially trying to describe is that the objects should not reveal their internals to the outside world (other objects). They should just provide an interface for the world to tell them what needs to be done. All the details of *how* they achieve the tasks that are *told* to achieve it's *their* business and no one else's.

In a technical level, an object exposes a set of public methods (API) and probably uses variables and data structures to manage it's state and perform the tasks that it's told to perform.

> Encapsulation mandates that the state of the object should be kept private, unknown to the external world.

# The problem with `getters` and `setters`

This is exactly where `getters` and `setters` enter the picture. Conventional wisdom has it that since the object's variables are to remain "hidden", they should be wrapped by a `getter` and `setter` each, enabling the external world to "access" them, without learning about the state's object. Now, pause for a minute and read this last sentence again before proceeding. *Does it make any sense at all?* At the end of the day, what difference does it make if we are to use the variables either directly or using their wrapper `getter` and `setter`? Essentially we are messing with the object's state - which is quite overtly exposed to the public via these methods - in either case.

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

However, all we do is constantly manipulating the object's state, essentially implementing the logic that it should possess. We are *micromanaging* the object. Instead, we should *trust* it on knowing how to do its job. We keep on **asking** about it's state and then modify it instead of **telling** it the end result that we wish. Conforming to OOP, all we need to do is to *send it a message*, like the following

```
airCondition.adjustTemperatureTo(25)
```

and it should get the job done, because it *knows* how to actually do it.

# Tight coupling

We all know (at least in principle) that our classes should be highly cohesive and loosely coupled. The theory is great, but let's consider how these guidelines apply to this specific example. Let's assume that we wish to refactor the `AirCondition` class. Perhaps we would like to rename the `temperature` variable to `currentTemperature`. Performing this elementary refactoring move, would create a chain reaction, causing all the classes that depend upon it (its collaborators) to fail to compile and impose the need to refactor them too. Perhaps, some collaborators of these collaborators should be refactored as well and so forth.

This scenario illustrates perfectly the side effects of a design with tightly coupled classes. However, on the second, the *imperative* approach, the collaborators of the refactored, `AirCondition` class would remain unaffected, agnostic to the modification (given that the public API of the class was not modified). We can therefore conclude that the imperative approach has led to a more loosely coupled design.

# Tell, don't ask

Some of you might have already noticed that these ideas start to sound a lot like the *Tell, don't ask* principle (also known as *Law of Demeter*). (In case you're not familiar with this principle, feel free to look it up online as I will not delve into its details in this post). The essence behind the principle, which is in total accordance with the previously expressed ideas is that objects are not to be treated as data structures. Splitting the data and the logic to act on these data in different objects is not wise.

> Data and functionality that depends on these data belong in the same object

# A story and a lesson learned

Once, while working for a company heavily based on microservices, I had to implement a small feature in a microservice I wasn't normally contributing to. While studying the code I quickly realized that it was a common practice to access class properties directly. I actually walked into a tech leads meeting trying to explain both what encapsulation is and why it would be beneficial to use it, via `getters` and `setters`. Eventually, I failed to pass the message (at least adequately enough to initiate a change), which made me sad, but what made me even sadder was the realization, later in my life, that even if I had convinced this group of people to start using `getters` and `setters`, essentially not a thing would have changed in terms of the quality of the code and the product.

At the end of the day, what difference would it make to use `airCondition.getTemperature()` instead of `airCondition.temperature`? Perhaps that is the reason why the designers of Kotlin decided to provide `getters` and `setters` by default, without even going into the trouble to code (generate) them or even call(!) them (in Kotlin `airCondition.temperature` actually calls `airCondition.getTemperature()` under the hood).

# Conclusion
