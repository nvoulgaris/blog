---
title: "Test behavior, not implementation"
date: "2018-05-11"
tags: [unit-testing]
image: img/posts/shopping_cart.jpg
---

Over the years, I have identified a number of issues with the way most companies treat their tests. I have come to believe that the most important one is that test code is treated as a second class citizen. Developers usually opt for the cheap, quick-and-dirty solutions when it comes to writing (or maintaining) tests, not realizing its importance. However, test code has to be *designed*, *reviewed* and *refactored*, exactly like production code. What we usually fail to realize is that the way we write tests reflects on the *quality* of our production code, allows *bugs* to creep in and drives *design* decisions.

# Two approaches

In this post I will delve into the topic of *testing behavior* as opposed to *testing implementation*. So, let's elaborate a bit on these two fundamentally different styles. When testing behavior, we're thinking:

> I want to verify that, under these circumstances, the result of an action is correct

Testing for state on the other hand, means thinking:

> I want to verify that, under these circumstances, the result of an action derives from these things

Obviously, the approach is utterly different, but the gold is to understand the consequences of following one or the other. Before we work the trade-offs, let's illustrate the two styles via a simplified example.

# Example

Assuming we have a method that fetched all employees from the database, calculates their average salary and sends an e-mail with this number on the subject line. A *test-implementation* logic could lead us to verifying that the number of the fetched employees is correct by checking a list data structure size, the correct employees with the correct salaries are retrieved, the average salary is correct after taking into consideration each employee etc.

On the other hand, a *test-behavior* mentality would probably result in executing the method and checking that the `send()` method was executed in the e-mail service collaborator with the correct argument for the `subject` parameter.

# Trade-offs

We should always keep in mind that when it comes to software engineering, there is no silver bullet. A great part of our job is to recognize the trade-offs when they present themselves and decide responsibly, living with the consequences. Having said this, both approaches would work, leading to - most probably - different implementations and different ramifications when it comes to flexibility and maintenance.

## Refactoring

One of the most common pitfalls is to couple too tight our tests with the production code. What would happen in the first approach (test-implementation) when, in the future we decide dump the list and use a different data structure? Our test (that asserts on the list size and contents) will fail to compile. We will be forced to refactor the test along with the production code, immediately jeopardizing our whole refactoring process. Let me elaborate on this topic.

> When refactoring a piece of code, we intend to alter its structure but **not** its behavior.

In order to do so, given that the result of any action under the same circumstances remains unaffected, we should be able to rely on our tests to know that we did not change the behavior indeed. However, if we modify our tests, we run the risk of unwittingly modifying what we're testing, allowing bugs to creep in the production code.

We may stay clear from this danger applying the test-behavior logic. In this case, the tests do not "see" the actual implementation and since the results of the actions remain unchanged, the tests remain unchanged and we can make sure we keep them green in each and every refactoring move we make.

# Ripple effects

In my blog post on [unit testing best practices](https://nvoulgaris.com/unit-testing-best-practices) I referred to *isolation* as key property of unit tests. I stated that if a test fails, *"it should clearly declare a single aspect of the software that is not functioning properly and point us to it immediately"*. In this post I was referring to leaving the system in the state that we found it, but the isolation principle may be violated in other ways too.

when testing the implementation, we usually instantiate all the collaborators of the class we're testing, whereas, when testing the behavior we tend to use test doubles. A side effect of this is that if a bug lies in a collaborator of the class under test, its tests will will remain unaffected in the latter approach, but will fail in the former, creating a ripple of failing tests. Among other things, this will lead us into a debugging session in order to understand what is wrong with the system (as opposed to a finger pointing to the - carefully chosen - name of the failing test).

# Design decisions

These two different schools of thought reflect on
