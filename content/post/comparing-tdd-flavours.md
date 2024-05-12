+++
title = "Comparing TDD flavours"
date = "2019-03-25"
tags = ["TDD","XP"]
image = "img/posts/tdd_flavours.jpg"
description = "Chicago vs London"
+++

A few days ago, right after my talk/demo on hands-on Test Driven Development (TDD) on the JHUG meetup, I noticed that a lot of conversation was about applying TDD in real world systems. Somehow people felt that it was great for a short demo or for implementing a small, algorithmic piece of code, but could not see how it could be applied to a greater scale.

Conversation quickly shifted to Outside-In TDD and I decided to try and organize my thoughts concerning the two approaches. Timing couldn't be better. Having just finished watching an exceptionally good [clean coders series](https://cleancoders.com/videos/comparativeDesign) on the comparison between the two TDD styles, I had already decided to blog about it.

Therefore, after giving a very brief overview of the two approaches, I will attempt to describe their strengths and weaknesses according to my opinion.

## Overview of the techniques

There is no way I can thoroughly describe the two approaches in such a short post, but this isn't the intention here anyway. However, I feel that a very brief overview would facilitate in understanding the points that I am about to make. There is plenty of sources online explaining in detail both techniques, so please, feel free to consult them prior to continuing if needed.

### Classicist (Chicago school)

Classicist TDD requires that we lock ourselves in the red-green-refactor cycle, pushing requirements in the form of failing unit tests (red), implementing an increment to fulfill these requirements (green) and then working on structuring the code in a better way (refactor).

This approach attempts to *minimize mocking* and most of the *design happens at the refactor step*, having already implemented a working increment.

### Outside-In (London school)

Outside-In TDD uses a different approach. An extra step is inserted in the TDD cycle, the one of writing a failing *acceptance* test. So, we first focus on writing a failing acceptance test and then on locking ourselves in the above mentioned TDD cycle, for every class needed, until the requirement of this acceptance test is fulfilled. Focusing on one acceptance test at a time, we TDD our way from the outmost layer of the system (controller, queue consumer etc) all the way to the core (domain, database layer etc).

Some principal differences with regard to the previous approach are that *mocking and stubbing are heavily used* and most of the *design decisions are made in the red state*, allowing for more minor adjustments in the refactor step.

## Where I stand

It is reasonable for one to wonder whether I am biased on the topic or not. So, please allow me to clarify it before I proceed.

In my early TDD steps, I was mainly influenced by Uncle Bob and therefore, I started off as a classicist TDDer. After a considerably big learning curve, I started to like TDD a lot, but I was not *thrilled* by it. I always felt that the technique was great, but its professional application was limited and the benefits not always tangible (at least in my mind).

This changed radically the day I attended Sandro Mancuso's excellent *"Crafted design"* workshop. Despite my obvious shortcomings during the workshop, I loved the idea and I followed up hard and persisted until I was able to apply Outside-In TDD professionally and eventually transfer knowledge within my company and influence colleagues. I was finally thrilled and enthusiastic about applying TDD professionally and, frankly, ever since I did, I find it very hard to work in a different way. So, this is where I stand. *I love Outside-In TDD*.

Having said that, I have come forward with my bias before delving into the topic on purpose. I wanted to state where I stand and clarify that I will *not* let it impede my judgement.

## Comparison

Let me start by clarifying that the two TDD styles *are not mutually exclusive*. A skilled software engineer should ideally switch between the two, adapting to the situation in hand. However, I do feel that there are considerable strengths and weaknesses in each one and to the analysis of these is where I will focus for the rest of this post.

### Classicist

#### Strengths

##### Enables refactoring through loose coupling and contra-variant structure

An undeniable, powerful advantage of classicist TDD is that tests are loosely coupled to production code. The lack of mocking (and therefore stubbing) leaves the tests with a minimum amount of knowledge of *how* is the production code achieving *what* it needs to achieve. This enables even bold refactorings, using the unit tests as a safety net throughout the process. After all, as already mentioned above, important design decisions are made in the refactor step in this approach.

This refactoring ability is enhanced by the contra-variant structure of the code. Instead of having a test class per production class, the two structures are independent. This is achieved by testing public APIs, letting implementation details hide behind these APIs. This empowers refactoring even more, as even serious refactoring moves (like deleting whole classes for instance) would most likely not lead to broken tests.

Remember that during refactoring we want a steady, fast-executing suite of tests to verify **after every refactoring move** that we indeed only *changed the structure* of the code and *not its behavior*. I have articulated my arguments on this on my *"test behavior"* [post](https://nvoulgaris.com/test-behavior)

##### Delayed design decisions

Another strong quality of the classicist TDD that I like a lot is that design decisions are delayed as much as possible (if only we all did more of this). This follows logically from the fact that we first make it work (red to green) and then we think about how to make it better, doing most of the design in the refactor step, as stated more than once earlier. Delaying design decisions is one of the qualities that makes us truly agile (as opposed to lots of sticky notes, but that is another post once again - see [agile code](https://nvoulgaris.com/agile-code)).

#### Evolutionary design

In the classicist approach we start off small in terms of design and as we grow the code base to accommodate more requirements, we continuously refactor the code to adjust the design. This line of thought complements the delayed design decisions characteristic and binds excellently to the agile mindset. Together, they embrace the [YAGNI](https://en.wikipedia.org/wiki/You_aren%27t_gonna_need_it) principle and therefore, premature design decisions and over-engineered solutions are avoided. Instead, at any given moment, the design reflects the current needs of the application.

#### Weaknesses

##### Reduced test readability

I am a big fan of the triple A rule (Arrange-Act-Assert) and part of the reason is that the test reads like a state machine, fulfilling its *documentation* purpose. Ideally, I like 3-liner unit tests (one line for every stage), maximizing both *readability* and *communication of intent* (method extraction can help us make almost every unit test a 3-liner).

With the classicist approach I find that tests tend to grow large quite often, with complicated setups and assertions, which in extreme cases can defeat the whole documentation purpose (there is the name of the test to partially save this). This was definitely one of the notes I made while watching the clean coders comparative case study video series. Uncle Bob's tests were lengthy.

##### Complex refactorings

Since we are trying to flesh out the whole system starting from its core logic, it is quite probable to find ourselves in a situation where a class, deep inside the core of the application, has too many responsibilities or its design is cumbersome. Such cases, sometimes require *drastic* refactoring moves.

Complex refactorings are never pleasant and the more complex they are, the more the likelihood of breaking the tests increases. Usually, I find it much more preferable to apply small refactoring tweaks than tearing the whole system apart, while trying to keep my tests green.

##### Treating the API as a second-class citizen

Starting from the core logic of the application poses an extra problem. Thinking of the API is usually deferred until the implementation reaches it. One may argue that this is not a drawback, but we should always keep in mind when building a system that we do so **only** because someone else needs to use it. If we are writing a web service for instance, some client will consume this API, otherwise we wouldn't be writing it in the first place.

Therefore, I regard this as a considerable problem. We are running the risk of over-engineering our solution, implementing logic that will not be used. Don't get me wrong here. Creating abstractions and achieving loose coupling between our HTTP layer and our domain is very much desired. I just find it really useful to begin my thinking from the API.

I am really sitting on the fence regarding Uncle Bob's abstraction decisions on the clean coders comparative case study video series, leaning a little bit towards considering them premature and therefore potentially harmful.

### Outside-In

#### Strengths

#### TDD as a design tool

One of the principal differences between the two approaches is in which state most of the design decisions are made. While in the classicist approach this is happening in the refactor state, in Outside-In the answer is the red state. When writing a failing unit test, we have to think ahead of ourselves and *design*. We have to decide *what are the collaborators of the class under test going to be* and *how is this class going to communicate with them (public API) to fulfill this business requirement (test)*. These are core design decisions and are made *before* the implementation. Of course, design can be refined in the refactor step, but usually, in a much more light way.

Despite some objections on this (more on this later on), I love the way TDD is really used as a design tool. During the JHUG talk/demo we discussed on how TDD does not magically create good design by itself. TDD gives us the time and place to design and this is done brilliantly in the Outside-In style.

##### Acceptance tests drive the architecture

Earlier, I made the point how using the classicist approach can result in treating the API as a second-level citizen. I feel quite the opposite when using the Outside-In approach. Not only we start off with the HTTP layer, but the needs of this layer drive the rest of the implementation and architecture all the way to the classes deep inside in the domain. The whole system is built in a way that serves the clients' needs and therefore its purpose. Of course, we are free (and in fact encouraged) to create the right abstractions and seal our implementation, without compromising our attention to the API.

##### Adopting the client's point of view

While running our inner TDD cycles we are very diligent in mocking all the dependencies of the class under test and put a lot of thought in the stubs that we will use. As mentioned earlier, this is in fact *design*. What I particularly like about this design method is that we always focus on the way the clients of these mocked classes will interact with them. We are designing their public API, allowing ourselves to *hide* the implementation details behind this public API when the time comes to implement this class.

What is so brilliant about this though process is that we always approach a new class from the point of view of its clients. We first think what kind of **behavior** we would like this class to provide in order to fulfill which business requirements (tests).

##### Test readability

As opposed to the classicist approach, I love the way the tests read in Outside-In TDD. Arrange, act and assert are evidently separated, tests are relatively short and the intent is clearly expressed in a *state-machine* manner. Also, taking the *"should"* naming convention (which I *absolutely* love) into consideration, the executable documentation produced is all that one could ask for.

##### Method and discipline

I left for last what I perceive as a vague, less objective advantage. When writing code using the Outside-In TDD approach, I always feel that there is method and discipline in my work. I feel that I am working very *methodically*. It is almost as if I am following an algorithm, approaching the problems in layers, breaking it down in small pieces and knowing exactly what needs to be done next and where am I in the whole process at any given moment. The acceptance tests acts like a north star that will not let you get lost while running the inner TDD cycles. This is mainly due to the fact that the way they fail will lead me to the point I have to pick up the implementation from when finished implementing a class.

I understand that this is utterly subjective, but I do not feel the same way when using the classicist approach. Throughout the clean coders comparative case study video series I always knew where Sandro was and what was missing for an API to be finished, but I always had to think harder when Uncle Bob was driving the implementation.

#### Weaknesses

##### Refactoring limitations

Throughout my journey to understand and adopt the Outside-In TDD style, I always struggled with the refactoring limitations that are posed by following this technique. In a nutshell, the mocking and stubbing that are heavily used result in tight coupling between the production and test code, with severe implications to refactoring capabilities.

This caused me great unease until I truly understood the *deviation in the philosophy* between the two approaches. In the classicist approach emphasis is first put on making it work and *then* on the structure of the code. Therefore, the room for refactoring in the refactor step is *created* because it is *needed*, given that this is where we largely shape the structure of the code. On the other hand, with the Outside-In approach, we focus on structure from the beginning, leaving less room for modifications in the refactor step since we *anticipate less major modifications*.

It does take some time to truly understand this differentiation in the way of thinking, but as soon as one does get it, it's all very clear. In my perception, a profoundly uneasy state to be in is thinking in classicist terms (I will structure the code in the refactor step) when trying to apply Outside-In TDD.

##### Not suitable for algorithmic code

As this approach focuses on *dependencies* and *collaboration* between classes, is follows logically that it is not an ideal candidate for implementing an algorithmic piece of code. Usually, there are no collaborators in such a case and therefore this technique will be of limited use. Therefore, this constitutes a perfect example to demonstrate cases in which we should switch to a different TDD style, such as the classicist one.

## Conclusion

TDD is a very handy tool to have in our arsenal and if we intend to be true *software craftspeople*, this arsenal better be mighty and better include both TDD styles. We ought to study and apply both of them and draw our own conclusions as to which one we favor in which situation and why.

In my opinion, judging based on the problem in hand is crucial and ideally we should learn to switch between the two. Don't forget that in software engineering almost everything is a trade-off and working these trade-offs is what makes us better *professional* software engineers. There is no silver bullet for most problems and - despite personal preferences - TDD styles is not an exception.
