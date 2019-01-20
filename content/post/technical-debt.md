---
title: "Dealing with technical debt"
date: "2019-01-17"
tags: [technical debt,agile]
image: img/posts/encapsulation.jpg
---

# What is it

# Where does it come from

There are numerous and very diverse ways in which technical debt can be created. Some are easier to spot and even prevent. Some are quite tricky and some are inevitable.

## Unprofessional technical debt

An easy to spot (and prevent) way of incurring debt is not taking the time to do our job in the right way. Every time we opt for a *hack*, a *quick-and-dirty* solution, a *workaround*, every time we *skip some unit tests* or *do not refactor* the code, we create debt. Every time we are sloppy with our work because someone says that *"this is urgent"* or *needs to be done by today* and we succumb to this pressure, we create future troubles for our team and our organization.

> Every time we cut corners, we create technical debt

I am trying to put as much emphasis as I can and be harsh with this. Coming up with a way to improve code or identify weaknesses is not only natural, but welcomed, especially as we become more mature. However, *wittingly* applying discounts - therefore creating this type of technical debt -  is, in my opinion, absolutely **unprofessional** and **irresponsible**. Deliberately undermining our code quality to reduce time to market is an approach that will come back and bite us in the future. Period.

## Outdated design technical debt

Sometimes we start of with simple and robust design and architecture for the initial requirements of the system, but as time goes by and increments are added, we fail to adjust the design and architecture in a proportional way. This phenomenon is more likely to occur when new developers join the team and do not fully understand the original design.

While this can be prevented as well by taking the time to develop the architecture as we develop the system, it is not unlikely at all that even by incrementally refactoring, at a certain point we will realize that we are in need of a drastic refactor.

## Software grew old technical debt

Technology races forward in an astonishing pace these days and therefore we may find ourselves with a dependency that will become deprecated in the upcoming release (a database driver for instance). There is not much we can do about it and no one is to blame really. We should just take the time to keep our dependencies up to date. If we do it proactively instead of waiting for a deprecation announcement, even better.

# There will always be technical debt

Of course, trying to always be tech debt free is simply delusional. Databases deprecate their old driver versions, systems grow enough to require that architecture should be revised and no matter how exceptionally we write a piece of code, as we grow more experienced and knowledgeable, we will always identify weakness and better ways to write it.

> If we look back to a piece of code we wrote a year ago and find nothing that we would do in a different, better way today, perhaps we have remained stagnant for the past year.

So, technical debt will present itself no matter how professional and diligent we are.

# And it's OK

This is a fact and we have to accept it. After all, we should always bear in mind that the iterative nature of shipping software is built on the foundation of feedback. We solve the problem, we deliver the solution, get feedback on it and then try to improve it. Trying to ship a *perfect* product will result is a tail chase.

Technical debt, comes hand in hand with agile products and innovation. Sometimes we have to prototype solutions. Most of the times we have to get a feature out quickly, just to get feedback and learn what the users really want (after all they usually don't know what they want either, until they have a prototype to play with). This will create technical debt and we have to find our peace with it and embrace it.

Of course, this is fundamentally different from ignoring it and just letting the code rot. On the contrary, it is something that should be dealt with, because it costs. And it costs a lot.

# How costly is it

The spectrum of ways in which technical debt can hurt a team or a product is surprisingly wide. I chose to discuss some of the most important ones, according to my opinion.

## Development slows down as time goes by



## Reduced quality
Bugs, System Performance

## Demoralization

I saved the most sneaky and costly one for last. Chances are that a well taken care of piece of code will remain so and future software engineers that will touch it will go to great lenghts to keep its quality high. On the other hand, sloppiness and low quality propagate tremendously fast within a code base. A badly written, poor quality, piece of code will most likely tempt the next software engineer to work on it to opt for a hack, or a quick-and-dirty solution. Andy Hunt and Dave Thomas use a great metaphor of a broken window to describe exactly this in their book, ["The Pragmatic Programmer"](https://www.goodreads.com/book/show/4099.The_Pragmatic_Programmer).

The poorer the quality, the faster more and more technical debt will accumulate, *demoralizing* the team and rendering the code a nightmare for any software engineer. This is a typical situation, which, more often than not, results in the best people leaving the project (usually the company as well) and set off for new adventures. This is not only costly for the project, but for the organization as well.

# How to deal with it

Having said all these, how are we going to approach such a tricky situation? The stakeholders definitely will not ask us to take time address the technical debt.

Mapping it to actual value can be a solution, but it usually turns out to be quite difficult. For instance, updating the database driver can improve the performance of the application, but how can we transform this into a measurable, well defined PBI (Product Backlog Item) or user story that presents business value? How faster is the application going to be and how beneficial is this to the business anyway? Even if this can be achieved, how about refactoring to improve the application's design? There is no way we can present immediate business value out of it. But it does reflect to the business value in a shocking way.

My proposal is the following: Reserve a corner of your scrum board for technical debt. Have every team member that comes across technical debt, write a sticky note about it and stick it to this corner. Also, take some to discuss about it with the rest of the team (perhaps in the upcoming daily scrum). During planning, take this debt corner into consideration. When asked to refine, estimate or plan a PBI that (even remotely) touches an area with technical debt, include this debt sticky note in the PBI.

This method will not only make the team address technical debt in the first chance, therefore keeping the code in a relatively good shape. It will also facilitate in working with the stakeholders to educate them on the value of software quality. The latter may sound minor in comparison to the former, but sometimes it is the greater good between the two.

# Conclusion




???

* Map tech debt reduction efforts to measurable customer outcomes
* Use powerful metaphors
* Take responsibility as Developers
* Use Code Metrics to quantify Technical Debt
* Make Technical Debt transparent on the Product Backlog

Iceberg photo?

https://productcoalition.com/how-great-product-managers-deal-with-technical-debt-453edec3d473
