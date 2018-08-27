---
title: "How much code coverage should I have?"
date: "2018-08-27"
tags: [unit-testing,code-coverage]
image: img/posts/code_coverage.jpg
---

One of the most disturbing questions I often get refers to the percentage of the code that should be covered by unit tests. This is a perfectly fine question coming from a fairly inexperienced developer, but it troubles me greatly in virtually any other case. However, what urged me to write this post is that I gradually become aware of more and more organizations that actually impose rules on this metric. Rules like "the project *must* have 90% code coverage".

Now, there is a number of issues with this kind of approach. What if we get a 99% code coverage and we keep on getting bugs regularly? Does this 99% reflect code quality? Is it wise to impose rules on the developers, forcing them to reach a certain number on the metric? Can one write a suite of tests that cover all the code, but essentially test *nothing*? Is this meaningful? and more importantly, **why** are we testing in the first place?

Before we delve into the topic, let me clarify the following: practicing TDD as a discipline means that code coverage should approach 100% (but never quite reach it actually). However, since this post does not refer only to TDDers and even applying TDD won't result in a 100% code coverage (one can easily understand this taking into consideration configuration files, Data Transfer Objects etc), I would like to take a more pragmatic view and discuss on the mentality behind all these.

# Example

Allow me to begin with an example that will help us understand the nature of the problem at hand. Let's consider the following, very simplistic function that performs division between two integers (it's hardly reasonable to assume that anyone would need such a function, but let's consider it for the sake of the argument).

```
public int divide(int a, int b) {
  return a / b;
}
```

How many tests should we write for this function? Which tests should these be? It's fairly obvious that a single test would result in a 100% code coverage for this one-liner. Is this sufficient? Now let's take a step back and reflect for a moment.

> How many states can this piece of code be in?

A state would be a = 1 and b = 1. A second state would be a = 1 and b = 2 and so forth. Therefore, the combinations of all the possible values of variables `a` (the numerator) and `b` (the denominator) gives us the answer. Assuming that `a` and `b` are both java integers, each can take a bit over 4 billion values. Therefore, the states that this piece of code can be in are 4.000.000.000 squared!

Hopefully, by now, my point is illustrated. *It's very easy to reach 100% code coverage and yet, we have tested only 1 out of 4.000.000.000 squared states*.

# Meaningful testing

Having understood the problem, what should one do? Opt for trying to test each and every state is clearly not only insanity, but very wasteful too. On the other hand, staying rest assured with the impressing 100% code coverage, created by the first test, is clearly not the right option either, since, clearly, a very problematic set of states remain untested: the ones when `b` (the denominator) is equal to 0.

Enter on of the most important virtues of unit testing: *meaningfulness*. Coming back to the previously asked questions, I believe that testing a couple "regular" cases and one with the denominator equal to 0 (I guess, expecting an `ArithmeticException` to be thrown) makes sense and is probably what most software engineers would do.

However, consider our choice of tests. Can anyone actually *prove* that these tests suffice to cover this piece of code? Is there a *mathematical formula* that can produce this set of tests as the *right* answer to the question of how many and which tests should we write? Absolutely **no**. Can it be the case that we were actually careless and have missed a bug after all? Absolutely **yes**. This is nothing more than a *sensible* result, a **meaningful** suite of tests for this piece of code.

Of course, this example, being very simplistic, leaves almost no room for error. However, one can understand that in real world situations the margin for error is significantly increased and being meaningful in choosing the test cases takes a whole lot more importance. However, meaningful testing is not a quality some developers are born with and some other are destined to never possess. It's mainly built through trial and error and derives from experience. So, perhaps, next time you face a bug, take a moment to think why it wasn't covered with a unit test in the first place (by the way, also never forget to add that unit test, but this is another topic).

# Avoid meaningless tests

Quite often, the very constraint on a code coverage number can be very harmful. People tend to forget *why* are they testing and start writing tests just to satisfy the numbers. Junior developers get the wrong stimulae, which shape their careers in the wrong way.

Meaningless tests, tests that test *nothing* become part of the regression suite, polluting the project in a unique way. They may *fail frequently*, causing the developers to *ignore* them, causing a total lack of trust in the test suite, or, even worse, they may be *green all the time*, even when a defect is introduced to the system. In either way, credibility in the test suite is lost, refactoring becomes harder and harder and eventually the project rots.

# Follow the trend

Coming back to the situations where organizations enforce specific code coverage numbers - I hope that by now the fundamental problems that lie with this approach have become apparent - what would a sensible policy be? We're not actually suggesting that code coverage is totally useless, right? Of course not. On the contrary, it can be immensely valuable.

> How should it be used then?

This constitutes ground for experimentation and I would very much like to hear anyone's views on the matter. For now, let me describe an approach that I find useful. Start monitoring the code coverage and create a trend line metric for it. Make sure that, before merging a merge request, the line does not drop. If it does so, kindly ask the author to amend this, before merging the code. This can even constitute a condition in the team's DoD. I believe that a lot of CI tools will provide plug-ins that help implement this policy (personally, I have used Jenkins and JaCoCo).

# Untested code

Instead of missing the point and start chasing after numbers just for the sake of it, use code coverage as what it really is: a *tool*. Make sure you go thoroughly over the report (tools like JaCoCo produce an extremely detailed report) on a regular basis. This can point out quite a few interesting things, such as untested parts of the code. Identify them and act on them. Perhaps a pattern will become visible. Find the problem and address it.

# Quality testing

Getting fixated on the code coverage number will harm both the developers and the project they're working on in the long run. Instead of it, try to create a culture that focuses on quality testing. Make sure that the right tests are being written, the engineers start to gradually **trust** their test suite, enabling them to refactor the code as often as they find useful and bugs that slip into production become less and less. At all times, remember that:

> Low code coverage means that there are problems. High code coverage means nothing at all on its own.

# Conclusion

Code coverage is a great **tool**, but use it wisely. Stay clear from useless, arbitrary rules and constraints. Oppose yourself to them, no matter who imposed them, with grounds. Raise the coverage as high as possible, but as a result of responsible, meaningful, quality testing and think hard on any poorly tested (or even untested) areas. Focus on the ability to **refactor using tests as a safety net** and **catching bugs** as early as possible. As always, forget about the rules. Stick to the essence.
