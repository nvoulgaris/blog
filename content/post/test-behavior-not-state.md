+++
title = "Test behavior"
date = "2018-05-23"
tags = ["unit-testing", "software design"]
image = "img/posts/writing.jpg"
description = "Testing what is done vs how it's done"
+++

Over the years, I have identified a number of issues with the way most companies treat their tests. I have come to believe that the most important one is that test code is treated as a second class citizen. Developers usually opt for the cheap, quick-and-dirty solutions when it comes to writing (or maintaining) tests, not realizing their importance. However, test code has to be *designed*, *reviewed* and *refactored*, exactly like production code. What we usually fail to realize is that the way we write tests reflects on the *quality* of our production code, allows *bugs* to creep in and drives *design* decisions.

## Two approaches

In this post I will delve into the topic of *testing behavior* as opposed to *testing implementation*. So, let's elaborate a bit on these two fundamentally different styles. When testing behavior, we're thinking:

> I want to verify that, under these circumstances, the result of an action is this

Testing for state on the other hand, means thinking:

> I want to verify that, under these circumstances, these actions take place to reach to the result

Obviously, the approach is utterly different, but the gold is to understand the consequences of following one or the other. Before we work the trade-offs, let's illustrate the two styles via a simplified example.

## Example

Assuming we have a unit that fetches all employees from the database, calculates their average salary and sends an e-mail with this number on the subject line. A *test-implementation* logic could lead us to verify that the number of the fetched employees is correct by asserting on the size of a list data structure, the correct employees with the correct salaries are retrieved, the average salary is correct after taking into account each employee etc.

On the other hand, a *test-behavior* mentality would probably result in executing the method and checking that the `send()` method was executed in the e-mail service collaborator with the correct argument for the `subject` parameter.

## Trade-offs

We should always keep in mind that when it comes to software engineering, there is no silver bullet. A great part of our job is to recognize the trade-offs when they present themselves and decide responsibly, living with the consequences. Having said this, both approaches would work, leading to - most probably - different implementations and different ramifications when it comes to flexibility and maintenance.

### Refactoring

One of the most common pitfalls is to couple too tight our tests with the production code. What would happen in the first approach (test-implementation) when, in the future we decide to dump the list and use a different data structure? Our test (that asserts on the list size and contents) will fail to compile. We will be forced to refactor the test along with the production code, immediately jeopardizing our whole refactoring process. Let me elaborate on this topic.

> When refactoring a piece of code, we intend to alter its structure but **not** its behavior.

In order to do so, given that the result of any action under the same circumstances remains unaffected, we should be able to rely on our tests to know that we did not change the behavior indeed. However, if we modify our tests, we run the risk of unwittingly modifying what we're testing, allowing bugs to creep in the production code.

We may stay clear from this danger applying the *test-behavior* logic. In this case, the tests do not *"see"* the actual implementation and since the results of the actions remain unchanged, the tests remain unaffected and we can make sure we keep them green in each and every refactoring move we make.

### Ripple effects

In my blog post on [unit testing best practices](https://nvoulgaris.com/unit-testing-best-practices) I referred to *isolation* as key property of unit tests. I stated that if a test fails, *"it should clearly declare a single aspect of the software that is not functioning properly and point us to it immediately"*. In this post I was referring to leaving the system in the state that we found it, but the isolation principle may be violated in other ways too.

When testing the implementation, we usually instantiate all the collaborators (dependencies) of the class we're testing, whereas, when testing the behavior we tend to use **test doubles**. A side effect of this is that if a bug lies in a collaborator of the class under test, its tests will remain unaffected in the latter approach, but will fail in the former, creating a **ripple of failing tests**. Among other things, this will lead us into a debugging session in order to understand what is wrong with the system (as opposed to a finger pointing to the - carefully chosen - name of the failing test).

### Design decisions

As I have mentioned earlier in this post, *tests drive design decisions*. This is an immensely important point, so let me repeat it. *Tests shape our production code*. I am mostly referring to Test Driven Development here, but we should always refactor a piece of code that is difficult to test, irrelevant of *when* the tests where written. Therefore, the tests affect the production code even if we don't test-drive it.

Before we elaborate, let's tale a step back to consider a basic unit testing tool: **test doubles**. [Gerard Meszaros](https://www.goodreads.com/author/show/193408.Gerard_Meszaros) uses this term to describe *an object that is used in place of a real object for testing purposes*. Two test double types that we're particularly interested in (for the purposes of this post) are the following:

 * **Stub**: In advance specified behavior covering *specific answers to specific calls*. This is done in order to serve the test and no additional behavior is prescribed.
 * **Mock**: Specified *expectations* referring on the *reception of specific method calls* (potentially with specific arguments)

Now, these two different test doubles are mainly used by two different schools of thought.

 * **Classical TDDers** will use *real instances of every collaborator* involved in the test. When this is either inconvenient or too difficult, a test double will be used, usually a **stub**.

 * **Mockist TDDers** will *never instantiate another class* besides the one which is under test. **Mocks** will be used instead.

These choices are utterly important. It is easy to understand that the more stubs we use, the more we couple our unit tests with our production code. This happens because, what we're essentially saying when stubbing a class is *"when this method is called with these arguments, do this"*. However, this method call is an implementation detail and should we wish to not call this method during a future refactoring, our unit test will fail (or at least will have to be refactored as well, in order to remove the unused stubbing).

In addition, a mockist TDDer will (via the usage of mocks instead of real objects) achieve a quite better (ideally perfect) isolation on the unit tests, as opposed to a classical TDDer, who will have to face a ripple of failing tests sooner or later.

One of the most important aspects of this topic though is that different choices (stubs instead of mocks, classical TDD instead of mockist TDD) will result in a totally different production code and a totally different code design. Therefore, **favoring testing behavior will produce a totally different application**, with different trade-offs, different advantages and shortcomings and different code quality. Hence, I believe that it has become apparent by now (if it wasn't already) that these are decisions that we have to thinking very carefully and take very seriously.

## Conclusion

My initial intention behind this blog post was to raise awareness. Test code should **not** be treated as second class citizen. There are loads of crossroads, decisions and trade-offs out there and I hope that I have made clear that the ramifications are very significant. Favoring testing behavior brings along a series of side effects and in any case, it is a road that, should we decide to follow it, we should do so wittingly and with professionalism.
