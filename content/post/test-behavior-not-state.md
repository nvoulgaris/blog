---
title: "Test behavior, not state"
date: "2018-04-30"
tags: [unit-testing]
image: img/posts/shopping_cart.jpg
---

Over the years, I have identified a number of issues with the way most companies treat their tests. I have come to believe that the most important one is that test code is treated as second class citizen. Developers usually opt for the cheap, quick-and-dirty solutions when it comes to writing (or maintaining) tests, not realizing its importance. However, test code has to be *designed*, *reviewed* and *refactored*, exactly like production code. What we usually fail to realize is that the way we write tests reflects on the *quality* of our production code, allows *bugs* to creep in and drives *design* decisions.

# The two approaches

In this post I will delve into the topic of *testing behavior* as opposed to *testing state*. So, let's elaborate a bit on these two fundamentally different styles. When testing behavior, we're thinking:

> I don’t care how you come up with the answer, just make sure that the answer is correct given these preconditions

Testing for state on the other hand, means thinking:

> I don’t care what the answer is, just make sure you do these things while figuring it out

Obviously, the approach is utterly different, but the gold is to understand the consequences of following one or the other. Before we work the trade-offs, let's illustrate the two styles via a simplified example.
