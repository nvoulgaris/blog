---
title: "Comparing TDD flavours"
date: "2019-03-19"
tags: [tdd]
image: img/posts/tdd_flavours.jpg
---

A few days ago, right after my talk/demo on hands-on TDD on the JHUG meetup, I noticed that a lot of conversation was about applying TDD in real world, production systems. Somehow people felt that it was great for a short demo or for implementing a small, algorithmic piece of code, but could not see how it could be applied to a greater scale.

Conversation quickly shifted to Outside-In TDD and I decided to try and put my thoughts in order concerning the two approaches. Timing couldn't be better. Having just finished watching an exceptionally good [clean coders series](https://cleancoders.com/videos/comparativeDesign) on the comparison between the two TDD styles, I already wanted to blog about it.

Therefore, after very briefly describing...

# Overview of the techniques

There is no way I can thoroughly describe the two approaches in such a short post, but this isn't the intention here anyway. However, I feel that a very brief overview would facilitate the reader. There is plenty of sources online explaining in detail the two techniques. Feel free to consult them prior to continuing if needed.

## Classicist (Chicago)

Classicist TDD requires that we lock in red-green-refactor cycle, pushing requirements in the form of failing unit tests in the red state, implementing an increment to fulfill these and then working on structuring the code in an efficient way.

This approach attempts to *minimize mocking* and most of the *design happens at the refactor state*, having already implemented a working increment.

## Outside-In (London)

Outside-In TDD uses a fundamentally different approach. The writing of a failing *acceptance* test is inserted in the classicist TDD cycle. So, we first focus on writing a failing acceptance test and then on locking ourselves in the above mentioned TDD cycle, until the requirement of this acceptance test is fulfilled. Focusing on one acceptance test at a time, we TDD our way from the outmost layer of the system all the way to the core (e.g. database).

Some principal differences with the previous approach are that *mocking and stubbing are heavily used* and most of the *design decisions are made in the red state*, allowing for more minor adjustments in the refactor step.

# Where I stand

Before I proceed, It is reasonably to wonder whether I am biased on the topic or not. So, please allow me to clarify it.

In my early TDD steps, I was influenced by Uncle Bob and therefore, I started off as a classicist TDDer. After a considerably big learning curve, I started to like TDD a lot, but I was not thrilled by it. I always felt that the technique was great, but its professional application was limited and the benefits not always tangible (at least in my mind).

This changed radically the day I attended Sandro Mancuso's excellent *"Crafted design"* workshop. Despite my obvious shortcomings during the workshop, I followed up hard and persisted until I was able to apply Outside-In TDD professionally and eventually transfer knowledge within my company and influence colleagues. I was finally thrilled, enthusiastic about applying TDD professionally and, frankly, ever since I did, I find it very hard to work in a different way. So, this is where I stand. *I love Outside-In TDD*.

Having said that, I have come forward with my bias before delving into the topic on purpose. I wanted to state where I stand and clarify that I will *not* let it impede my judgement.

# Comparison

Let me start by clarifying that the two TDD styles *are not mutually exclusive*. A skilled software engineer should ideally switch between the two, adapting to the situation at hand.

## Classicist

### Strengths

#### Enables refactoring through loose coupling and contra-variant structure

An undeniable, powerful advantage of classicist TDD is that tests are loosely coupled to production code. The total lack of mocking (and therefore stubbing) leaves the tests with a minimum amount of knowledge of *how* is the production code achieving *what* it needs to achieve. This enables heavy refactoring, using the unit tests as a safety net throughout the process. After all, heavy design decisions are made in the refactor step in this approach.

This refactoring ability is enhanced by the contra-variant structure of the code. Instead of having a test class per production class, the two structures are independent. This is achieved by testing public APIs, letting implementation details hide behind these APIs. This empowers refactoring even more as even tearing whole classes apart would not lead to broken tests.

Remember that during refactoring we want a steady, fast executing suite of tests to verify after *every move* that we indeed only change the structure of the code and not its behavior. I have articulated my arguments on this on my *"test behavior"* [post](https://nvoulgaris.com/test-behavior)

#### Delayed design decisions

Another strong quality of classicist TDD is that design decisions are delayed as much as possible (if only we all did more of this). This follows logically from the fact that we first make it work (red to green) and then we think about how to make it better, doing most of the design in the refactor state.

### Weaknesses

#### Reduced test readability

I am a big fun of the triple A rule (Arrange-Act-Assert) and part of the reason is that the test reads like a state machine, fulfilling its documentation purpose. Ideally, I like unit tests of 3 lines (one for every stage), maximizing both readability and intent communication.

With the classicist approach I find that tests grow large quite often, with complicated setups and assertions, which in extreme cases can defeat the whole documentation purpose in testing (there is the name of the test to partially save this). This was definitely one of the notes I made while watching the clean coders comparative case study video series. Uncle Bob's tests were lengthy.

## Outside-In

### Strengths

#### TDD as a design tool

One of the principal differences between the two approaches is in which state most of the design decisions are made. While in the classicist approach this is happening in the refactor state, in Outside-In the answer is the red state. When writing a failing unit test, we have to think ahead of ourselves and design. We have to decide *what are the collaborators of the class under test* and *how is this class going to communicate with them (public API) to fulfill this business requirement (test)*. These are core design decisions and are happening *before* the implementation. Of course, design can be refined in the refactor step, but in a much more light way.

Despite some things that I don't like about this (more on this later on), I love the way TDD is really used as a design tool.

#### Test readability

As opposed to the classicist approach, I love the way the tests read in Outside-In TDD.

#### Method and discipline

I left for last what I perceive as vague, less objective advantage. When writing code using the Outside-In TDD approach, I always feel that there is method and discipline in my work. It is almost as if I was following an algorithm, approaching the problems in layers, breaking it down in small pieces and knowing exactly what needs to be done next and where am I in the whole process at any given moment. The acceptance tests acts like a north star that will not let you get lost while running the inner TDD cycles and the way it fails will lead me to the point I have to pick up the implementation from when finishing with implementing a class.

I understand that this is utterly subjective, but I do not feel the same way when using the classicist approach. Throughout the clean coders comparative case study video series I always knew where Sandro was and what was missing for an API to be finished, but I always had to think harder when Uncle Bob was driving the implementation.

### Weaknesses

#### Refactoring limitations

Throughout my journey to understand and adopt the Outside-In TDD style, I always struggled with the refactoring limitations that are posed by following this technique. In a nutshell, a lot of mocking and stubbing is used, resulting in tight coupling between the production and test code, with severe implications to refactoring capabilities.

This caused great unease in my mind until I truly understood the *deviation in the philosophy* between the two approaches. In the classicist approach emphasis is first put on making it work and *then* on the structure of the code. Therefore, the room for refactoring in the refactor step is *created* because it is *needed*, given that this is where we largely shape the structure of the code. On the other hand, with the Outside-In approach, we focus on structure from the beginning, leaving less room for modifications in the refactor step since we *anticipate less major modifications*.

It does take some time to truly understand this differentiation in the way of thinking, but as soon as one does get it it allows for better sleep. In my perception, a profoundly uneasy state to be in is thinking in classicist terms (I will structure the code in the refactor step) when trying to apply Outside-In TDD.

# Conclusion
