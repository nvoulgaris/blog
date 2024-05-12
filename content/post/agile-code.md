+++
title = "Agile code"
date = "2018-01-20"
image = "img/posts/todo.jpg"
tags = ["agile","XP"]
description = "Understanding the essence of agile software engineering, past the superficial process changes"
+++

During Christmas, just a few days before I decided to take up blogging, I was reading Sandro Mancuso's excellent book [Software Craftsmanship](https://www.goodreads.com/book/show/18054154-software-craftsmanship). I couldn't help but agree (sometimes even out loud) when reading what Sandro describes as the Agile Hangover. How many companies decide to become *agile* only to find their projects failing for the very same reasons that urged them to become *agile* in the first place? What are the common characteristics of so many failed attempts? What is it that goes so wrong anyway?

## What is Agile anyway?

*Agile* is a notion so frequently used these days in the software engineering industry that has ended up being misunderstood. It would come as no surprise to me if one asked 5 people for the true meaning of this so called *agility* and gathered 5 different answers. Let me endeavor to explain the way *I perceive agile*.

Before *agile*, managers and (if lucky) representatives of the development team entered a meeting room in order to discuss (and agree on) any potential aspect and detail of an upcoming project, documenting everything. Then, the development team would come up with a plan to implement everything that document described. Therefore, they would "lock" themselves up, pursuing the coveted end state, which, of course, was thoroughly described in the document. After the implementation completion (which included a considerably large testing period), the outcome was delivered to the customer, finally engaging in a feedback loop, only to find out that - guess what - change was needed (let alone that half the features were not needed and would never be used). By its nature, this approach is cumbersome and does not embrace change. Locking yourself to a plan and blindly sticking with it jeopardizes becoming outdated with respect to new priorities. Think about it. How soon in the process can the customer realize that a change is needed? How can this be accommodated  in the above mentioned life cycle? How can this model deal with changing priorities?

In February 2001, seventeen people got together to discuss (what they perceived as) the problem in the way we build software and, by composing the *Agile* Manifesto, proposed a mindset centered around the creation of a short feedback loop. Therefore, the newly proposed idea proposed that we do not blindly stick to the (long term) plan anymore. We do a little bit of work, involve the customer seeking feedback, inspect the current state, adapt to the feedback and repeat the cycle.

>The way change is perceived is fundamentally altered, embracing it instead of considering it undesired. Now change is turned into an opportunity.

In my opinion, the key difference between the two approaches lies in the fact that *agile* detaches the software from the illusion of the end state. There is no end state. There will never be one.

>As long as the business is live, the software lives and evolves with it.  

## Making a company Agile

Being influenced is not a bad thing on its own. Blindly (or even worse, dogmatically) embracing a new idea is what I consider one of the greatest pitfalls out there tough. Being influenced is great, so long as one filters and challenges everything. Deciding to undergo the vast transformation that is required for a company in order to become *agile* needs to go through some extra filtering. Knowing *why* should it go after such a radical transformation and therefore, what is expected out of it are keys to the its success. Needless to say, just because it is trendy or some other company did it successfully do not suffice as reasoning. Sometimes, a bit of constructive criticism could be just what is needed to get us on the right track on understanding these *why* and *what*.

Usually, companies that haven't got into the trouble of clarifying these *why* and *what* prior to embarking on the transformation, find themselves hiring an *agile* coach who is supposed to magically move his wand, speak the right words and... boom! We're *agile* now. More often than not, a few months later, they find themselves with a shiny new process, but writing code in the exact same way and facing the same old problems. A few more months later, they find themselves wondering why this *agile* transformation did not pay off and why does it still take so long to solve a critical bug on production. Why is there a critical bug on production in the first place?

Don't get me wrong here. Changing the process is valuable, but we should never forget that the process is a means to an end. The goal is the software! In order to reach the standards we want in software, we should first change the process, but making sure that all along this brings a mindset shifting too. Perhaps hiring an *agile* coach was the correct move to make after all. However, he should be one with technical expertise, able to lead a mindset shifting, reflecting in the way that code is written in the company. As Albert Einstein would definitely point out, writing code in the same way and expecting different results just because we changed the process is pure insanity.

## Disciplines

During his keynote speech on Agile Greece Summit 2017, Uncle Bob (Robert Martin) talked about a set of disciplines that every developer should follow in order to seal our profession as best as possible from future misfortunes. He even gave us an oath. I will not give you any oath, but I would like to focus on a set of disciplines. Specifically, I would like to shift our attention to the disciplines that will improve the quality of our code. However, before we talk about quality, we should first make sure that we understand it.

Quality is a very hard to understand notion. What is quality after all? Can one measure it? In my humble opinion, despite the fact that quality is not a tangible entity there are signs that one can notice and know that the situation is improving (happier customers, decreasing maintenance cost, faster features development, less bugs in production just to name a few). I believe that in order to start noticing these sings, we should strive to adhere to a set of disciplines. Extreme programming (XP) comes with a powerful arsenal of practices that can get us on the right track. Let's briefly go over a few:

### Pair programming
If practiced right, it can be one of the most valuable assets of a development team. How many times have you heard a phrase like *"We have to modify and redeploy the payment module, but Chris is the owner of it and he's out of office today, snorkeling on the reef."*? Well, I guess we could either equip Chris with a waterproof mobile or struggle for **collective ownership** on our code.

Pair programming guarantees this result, along with a series of benefits like **improved code design, team cohesion, mentoring and fewer interruptions**. Unfortunately, people tend to just sit next to each other and believe that they are practicing pair programming. So, if you do practice it, make sure you do it right. Do you share a common keyboard? Does one focus on the big picture, reviewing every line that the other is typing? Do you trade roles frequently? Perhaps you play [ping pong](http://wiki.c2.com/?PairProgrammingPingPongPattern)? Do you learn from each other? How often do you switch pairs?

### Test Driven Development
How can we be *agile* if we don't have an automated suite of tests? If, instead of having self-testing code, manual work is needed to verify that the system behaves as expected? If there is not a single button to verify the whole application and sign it off for production? If testing the whole system requires hours? How *agile* can we be then?

TDD is a workflow that emphasizes on making us write **the best code that we can write** (by constantly asking *"can you make it better?"*"). If practiced right, it encourages **better design** (more cohesive and loosely coupled components), provides **documentation** (via executable examples, a.k.a. tests) and, when done with a feature, the **automated regression test suite** comes for free.

>As if the above mentioned are not sufficient, I could never stress enough the importance of [left shift](https://en.wikipedia.org/wiki/Shift_left_testing)

### Continuous integration
How quickly can we get our latest code, safely to production? How often do we have to integrate our code and face conflicts while doing so? *We should always be working on the latest version of  the code*. We should frequently push to our Version Control Systems (VCS) and check the code out in order to avoid delays and nightmare conflicts later on. Having a continuous integration system helps us work in a more *professional* way.

### Code review
At least two people should sign the code off. Review the code often. Make sure that the team trusts one another as it will free them to be relentless, which will only work to the team's benefit.

Use different review styles: over the shoulder review, pair programming or an official session, with the whole team present, dedicated to the task. Whichever the style, **review in essence!**

>Challenge the code design, propose alternatives and work the trade-offs that they present themselves.

Talk about performance, maintainability, business needs (without meaning that code formatting for instance should be neglected). Plan a review early enough to provide sufficient time to adapt to changes.

### Refactoring
Martin Fowler, in his wonderful book [Refactoring: Improving the Design of Existing Code](https://www.goodreads.com/book/show/44936.Refactoring), explains that before adding a new feature to our system, we should first ask ourselves if the current design of the system is ready to accommodate this new feature. If not, *we should refactor it*.

Create a suite of tests to act as a safety net, change the system in small steps (keeping the tests green in all steps) and make sure that the value of the software increases (other software engineers understand the code, maintenance is easier and development of new features is faster). Keep on doing so *mercilessly*, until the code meets the requirements.

Martin Fowler's [book](https://www.goodreads.com/book/show/44936.Refactoring) is an excellent read and despite being written around the time that the Agile Manifesto was being formed, the ideas in the book are remarkably relevant.

These techniques and practices are a few among many, and to go through them all exhaustively would be beyond the scope of this blog post. However, it is vital to understand that they are not an end in itself. The goal is to go out there and experiment with them. Study them and challenge them, but eventually pick the ones that enable us to improve the quality of the software that we produce. Adopt them and use them wisely.

## Conclusion

Being *agile* is trendy. This is not a bad thing on its own. Deciding to become *agile* just because it is trendy is truly one of the worst decisions an organization can make. We should investigate and understand the fundamental aspects that it touches before we decide to undergo such a radical transformation. Understanding that software does not have an end state is fundamental. On the contrary, it is like a living organization. It will keep on changing and we will constantly have to reform and reshape it to meet the ever changing business needs. As a matter of fact, the better it meets these needs, the more it will have to change (more feature requests, more traffic etc).

Becoming *agile* can be a great leap, but in order for it to be successful, we have to apply the changes deep down to the heart of our organization and not only to its skin. We have to change the mindset of the people and the way we write code. We have to write code in a way that embraces change, in the same way our shiny new process does. We have to go out there and search for the practices that best suit our needs, apply them, learn and start over.
