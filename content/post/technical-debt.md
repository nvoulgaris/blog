---
title: "Technical debt"
date: "2019-01-17"
tags: [object oriented design,encapsulation]
image: img/posts/encapsulation.jpg
---

# What is it

# Where does it come from

There are numerous and very diverse ways in which technical debt can be created. Some are easier to spot and even prevent. Some are quite tricky and some are inevitable.

## Unprofessional technical debt

An easy to spot (and prevent) way of incurring debt is not taking the time to do our job in the right way. Every time we opt for a *hack*, a *quick-and-dirty* solution, a *workaround*, every time we *skip some unit tests* or *do not refactor* the code, we create debt. Every time we are sloppy with our work because someone says that *"this is urgent"* or *needs to be done by today* and we succumb to this pressure, we create future troubles for our team and our organization.

> Every time we cut corners, we create technical debt

I am trying to put as much emphasis as I can and be harsh with this. In my opinion, this is the only type of technical debt that is **unprofessional** and **irresponsible** to create. Deliberately undermining our code quality to reduce time to market is an approach that will come back and bite us in the future. Period.

## Outdated design technical debt

Sometimes we start of with simple and robust design and architecture for the initial requirements of the system, but as time goes by and increments are added, we fail to adjust the design and architecture in a proportional way. This phenomenon is more likely to occur when new developers join the team and do not fully understand the original design.

While this can be prevented as well by taking the time to develop the architecture as we develop the system, it is not unlikely at all that even by incrementally refactoring, at a certain point we will realize that we are in need of a drastic refactor.

## Software grew old technical debt

Technology races forward in an astonishing pace these days and therefore we may find ourselves with a dependency that will become deprecated in the upcoming release (a database driver for instance). There is not much we can do about it and no one is to blame really. We should just take the time to keep our dependencies up to date. If we do it proactively instead of waiting for a deprecation announcement, even better.

# There will always be technical debt

Of course, trying to always be tech debt free is simply delusional. Databases deprecate their old driver versions, systems grow enough to require that architecture should be revised. Even the first type of technical debt will present itself no matter how professional and diligent we are. Even if we write the best cod that we can, in a few months we will (hopefully) be better software engineers and therefore able to solve the problem in a more elegant and effective way.

# And it's OK


# How to deal with it

Having said all these, how are we going to approach such a tricky situation? The stakeholders definitely will not ask us to take time address the technical debt.

Mapping it to actual value can be a solution, but it usually turns out to be quite difficult. For instance, updating the database driver can improve the performance of the application, but how can we transform this into a measurable, well defined PBI (Product Backlog Item) or user story that presents business value? How faster is the application going to be and how beneficial is this to the business anyway? Even if this can be achieved, how about refactoring to improve the application's design? There is no way we can present immediate business value out of it. But it does reflect to the business value in a shocking way.

My proposal is the following: Reserve a corner of your scrum board for technical debt. Have every team member that comes across technical debt, write a sticky note about it and stick it to this corner. Also, take some to discuss about it with the rest of the team (perhaps in the upcoming daily scrum). During planning, take this debt corner into consideration. When asked to refine, estimate or plan a PBI that (even remotely) touches an area with technical debt, include this debt sticky note in the PBI.

This method will not only make the team address technical debt in the first chance, therefore keeping the code in a relatively good shape. It will also facilitate in working with the stakeholders to educate them on the value of software quality. The latter may sound minor in comparison to the former, but sometimes it is the greater good between the two.

# Conclusion



- How costly it is
 * Performance
 * Development slows down as time goes by
 * Reduced quality

???

* Map tech debt reduction efforts to measurable customer outcomes
* Use powerful metaphors
* Take responsibility as Developers
* Use Code Metrics to quantify Technical Debt
* Make Technical Debt transparent on the Product Backlog

Iceberg photo?

https://productcoalition.com/how-great-product-managers-deal-with-technical-debt-453edec3d473
