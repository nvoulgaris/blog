---
title: "Dealing with technical debt in an agile environment"
date: "2019-01-25"
tags: [technical debt,agile]
image: img/posts/technical_debt.jpg
---

How many times have you experienced software engineering teams that, regardless of the reasons, opted for quick solutions, resulting in poor code quality and created problems that accumulated over time?

Eventually, the product resembles an iceberg. The stakeholders can only see the end result, the behavior of the system, the part of the iceberg that lies above the surface, unaware of what lies underneath it. However, the software engineers have the full picture. They know every aspect of the system and they understand the need to take some extra time to tide things up a bit more than the usual.

On the other hand, the stakeholders, happy with the current image above the surface, most likely will never request to devote effort (time and money) to get (what they perceive as) a perfectly working product to a better shape, especially in the short loops of agile software engineering, in which they expect tangible business value every few weeks.

It seems like a dead end, but a truly professional team of software engineers should never allow themselves to result in such a situation. It's their responsibility to be proactive about it. Let's take things slow though and discuss a little bit about technical debt.

# What is it

The term technical debt refers to all the things in a code base that could (and should) be improved, but do not directly affect the behavior of the system. It's the things that the software engineers know should be done in a different, better way, but chose to defer for the future.

> Technical debt is code written today that requires more effort in the future

This resembles a lot a bank loan, in which an individual gets money today that require more money in the future to pay off with interest, essentially creating debt.

The term *technical debt* is a metaphor, referring to quick-win software solutions that will slow development down in the future in order to pay the debt off. Also, since typically future amendments require more time than it would be originally required to provide a proper solution, the debt is incurred and paid with interest. Not paying the debt usually results in loosing the product, as the code base eventually becomes unmaintainable.

# Where does it come from

There are numerous and very diverse ways in which technical debt can be created. Some are easier to spot and even prevent. Some are quite tricky and some are inevitable.

## Unprofessional technical debt

An easy to spot (and prevent) way of incurring debt is not taking the time to do our job in the right way. Every time we opt for a *hack*, a *quick-and-dirty* solution, a *workaround*, every time we *skip some unit tests* or *do not refactor* the code, we create debt. Every time we are sloppy with our work because someone says that *"this is urgent"* or *"needs to be done by today"* and we succumb to this pressure, we create future troubles for our team and our organization.

> Every time we cut corners, we create technical debt

I am trying to put as much emphasis as I can and be harsh with this. Coming up with a way to improve code or identify weaknesses is not only natural, but welcomed, especially as we become more mature. However, *wittingly* applying discounts - therefore creating this type of technical debt -  is, in my opinion, absolutely **unprofessional** and **irresponsible**. Deliberately undermining our code quality to reduce time to market is an approach that will come back and bite us in the future. Period.

## Outdated design technical debt

Sometimes we start off with simple and robust design and architecture for the initial requirements of the system, but as time goes by and increments are added, we fail to adjust the design and architecture in a proportional way. This phenomenon is more likely to occur when new developers join the team and do not fully understand the original design.

While this can be prevented as well by taking the time to develop the architecture as we develop the system, it is not unlikely at all that even by incrementally refactoring, at a certain point we will realize that we are in need of a drastic refactor.

## Software grew old technical debt

Technology races forward in an astonishing pace these days and therefore we may find ourselves with a dependency that will become deprecated in the upcoming release (a database driver for instance). There is not much we can do about it and no one is to blame really. We should just take the time to keep our dependencies up to date. If we do it proactively instead of waiting for a deprecation announcement, even better.

# There will always be technical debt

Of course, trying to always be technical debt free is simply delusional. Databases deprecate their old driver versions, systems grow enough to require that architecture should be revised and no matter how exceptionally we write a piece of code, as we grow more experienced and knowledgeable, we will always identify weakness and better ways to write it.

> If we look back to a piece of code we wrote a year ago and find nothing that we would do in a different, better way today, perhaps we have remained stagnant for the past year.

So, technical debt will present itself no matter how professional and diligent we are.

# And it's OK

This is a fact and we have to accept it. After all, we should always bear in mind that the iterative nature of shipping software is built on the foundation of feedback. We solve the problem, we deliver the solution, get feedback on it and then try to improve it. Trying to ship a *perfect* product will result is a tail chase.

Technical debt, comes hand in hand with agile products and innovation. Sometimes we have to prototype solutions. Most of the times we have to get a feature out quickly, just to get feedback and learn what the users really want (after all they usually don't know what they want either, until they have a prototype to play with). This will create technical debt and we have to find our peace with it and embrace it.

Of course, this is fundamentally different from ignoring it and just letting the code rot. On the contrary, it is something that should be dealt with, because it costs. And it costs a lot.

# How costly is it

A team or a product can be severely hurt by technical debt in multiple ways. Unfortunately, these problems tend to steadily grow under the radar and only become visible when it's too late. Let's discuss the ones I believe are the worst ones.

## Development slows down as time goes by

What happens to a system when the code slowly rots? As Uncle Bob explains, it is becoming difficult to change. A single modification ignites a chain reaction that causes a cascade of modifications in dependent modules. The system is resisting to change. It is becoming *rigid*.

The more rigid a system becomes, the more development slows down. Gradually features  require more and more effort to be implemented. The stakeholders have to wait more to get value and features become more expensive.

## Reduced quality

To make matters worse, developing features in a rigid system is far more error prone. Introducing defects is more likely in a highly coupled, complicated, rotten design than in a clean, frequently refactored one. This reflects in reduced quality, which although cannot be measured, can be *felt* by the stakeholders. In extreme cases, this can even result in performance issues.

## Demoralization

I saved the most sneaky and costly one for last. Chances are that a well taken care of piece of code will remain so and future software engineers that will touch it will go to great lenghts to keep its quality high. On the other hand, sloppiness and low quality propagate tremendously fast within a code base. A badly written, poor quality, piece of code will most likely tempt the next software engineer to work on it to opt for a hack, or a quick-and-dirty solution. Andy Hunt and Dave Thomas use a great metaphor of a broken window to describe exactly this phenomenon in their book, ["The Pragmatic Programmer"](https://www.goodreads.com/book/show/4099.The_Pragmatic_Programmer).

The poorer the quality, the faster more and more technical debt will accumulate, *demoralizing* the team and rendering the code a nightmare for any software engineer. This is a typical situation, which, more often than not, results in the best people leaving the product (usually the company as well) and set off for new adventures. This is not only costly for the product, but for the organization as well.

# How to deal with it

Having said all these, how are we going to approach such a tricky situation? The stakeholders definitely will not ask us to take time address the technical debt.

Mapping it to actual value can be a solution, but it usually turns out to be quite difficult. For instance, updating the database driver can improve the performance of the application, but how can we transform this into a measurable, well defined PBI (Product Backlog Item) or user story that presents business value? How faster is the application going to be and how beneficial is this to the business anyway? Even if this can be achieved, how about refactoring to improve the application's design? There is no way we can present immediate business value out of it. *But it does reflect to the business value in a shocking way.*

My proposal is the following: Reserve a corner of your scrum board for technical debt. Have every team member that comes across technical debt, write a sticky note about it and stick it to this corner. Also, take some time to discuss about it with the rest of the team (perhaps in the upcoming daily scrum). During planning, take this debt corner into consideration. When asked to refine, estimate or plan a PBI that (even remotely) touches an area with technical debt, include this debt sticky note in the PBI.

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
