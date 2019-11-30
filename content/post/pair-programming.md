---
title: "Pair programming: making the sum greater than the parts"
date: "2019-11-30"
tags: [pair programming,xp]
image: img/posts/pair_programming.jpg
---

When was the last time that you did some pair programming?

# What is it

Pair programming is an extreme programming (XP) practice and, according to Kent Beck's book [*"Extreme Programming Explained: Embrace Change"*](https://www.goodreads.com/book/show/67833.Extreme_Programming_Explained), it is

> A programming technique where two people program with one keyboard, one mouse, and one monitor

So, essentially, two software engineers, working at the same task, in a single machine. Two roles are defined and used by the participants, ideally swapped frequently: the *driver* and the *navigator*.

 * The **driver** is writing the code, focusing on the task in hand and in the micro view of the code.
 * The **navigator** is constantly reviewing the code being written by the driver, is looking for logic problems and bugs and is thinking ahead of the architecture and design of the system, focusing on the macro view of the code.

# Why

Now, the first reaction of people that have not used the practice is skeptical, to say the least. After all, it sounds very counter intuitive at first. Why have two people doing the work that one of them would originally do anyway? So, let's talk a little bit about the benefits of pair programming.

## The sum is greater than the parts



## Collective code ownership

The more a team is practicing pair programming, the more it increases collective code ownership. When an individual writes a piece of code and then the team reviews it, inevitably, the author is implicitly perceived as the *"owner"* of this piece of code. Pairing defaults the [bus factor](https://en.wikipedia.org/wiki/Bus_factor) to 2 and increases collective code ownership, a vital quality for an agile team.

## More efficient
## Code is reviewed automatically

One of the greater benefits of pair programming is that the code is reviewed automatically, as it gets constantly reviewed by the navigator while is being typed by the driver. Taking into consideration that roles are swapped frequently, essentially the code is reviewed by the pair. Additionally, it is reviewed in a more active way, *driven by conversation and modifications*, instead of passively and silently reading a pull request without the author of the code. As a matter of fact, it is so well reviewed that it can be checked in and merged, although I would propose to open a pull request, have the rest of team have a look at it as well as have the pair take a more distant look after the work is done.

## Increased collaboration

Gone are the days that software was produced by individual sitting in their cubicles, working as isolated as possible. Nowadays, it is well understood that great software is delivered by great teams. Therefore, we focus our energy a lot into building great teams. Honestly, I can't think of a more catalytic action to this than having two people working together, on the same problem. Essentially, this boosts team energy like nothing else I have seen. Personally, as a scrum master, I always encouraged the team to work in pairs as much as they can and make sense.

## Learning opportunity

People say that code reviews is a great learning opportunity. I can't even begin to describe what a wonderful learning opportunity pair programming is. Honestly, I don't remember pairing without sharing knowledge. Sometimes sharing great software design ideas. Sometimes learning a keyboard shortcut or a small IDE feature. There's always knowledge sharing during pair programming.

## More difficult to cut corners

We do get tired when writing code. Especially, when solving hard problems. These are the moments when we get more prone to cutting corners. *"Let's skip this unit test"*. *"I could improve this, but let's leave it like this for now and I'll refactor in the future"*. We've all been there and it is quite natural when we grow really tired. We still know the right thing to do, but we lack the *discipline* to do it at this given moment. When working in pairs, cutting corners is more difficult. Usually, either the navigator will "push" towards the right direction or the driver will feel less at liberty to opt for a dirty solution.

## Less distractions

A software engineer works focused on a task, having built a mental diagram and his colleague asks "shall we go for lunch in 10 minutes?". Suddenly, the mental diagram is gone and 15 minutes are required to reconstruct it. Does anyone relate to such an incident? Writing code requires extreme concentration and we all know that interrupting a software engineer while writing code is a huge "no-no" (especially when wearing headphones). Fortunately, working in pairs decreases interruptions a lot. It is just more difficult to interrupt a pair than a single individual and people seem to think twice before it.

## Onboard a new team member

Do you remember your last onboarding a company experience? How long did it take you to become fully enabled and how did you go about it? Personally, I believe that working on a task and asking questions when stuck is a suboptimal approach. I find that pairing with a teammate is an excellent onboarding technique. As a matter of fact, I believe that pair programming is tailored made for onboarding new members. knowledge sharing is flowing in an unprecedented pace (both domain/business and technical) and there's also a deliverable coming of the process.

# How to pair program

Before thinking about roles and pieces of code, my advice is to focus on the setup. I find it critical that the screen is positioned in the center of the desk and both participants have equal access to it. Otherwise, you are running the risk of creating a situation in which one participant feels like a "guest" in the other's office, instead of an equal collaborator.

The second most important point, in my opinion, is having two keyboards, if possible. This contradicts the above-mentioned definition of pair programming, which talks about one keyboard, but I find it important remove the psychological barrier of actually having to "grab" the keyboard to contribute one line of code when needed.

Having taken care of the setup, I would suggest making sure that you swap roles frequently. This ensures that both participants stay engaged and focused and that their minds work on both the micro and macro view of the code. Having the same driver for a lot of time can end up with the navigator feeling marginalized and disengaged. There is no "right" amount of time, but, out of personal experience, I would suggest swapping every few minutes (20 the most). Of course, this is totally subjective and the pair can better find the window that works best for it.

Staying in the context of role swapping, when using Test Driven Development (TDD), I have found extremely useful the *"ping pong"* technique. According to this, the driver writes a failing unit test. Then, roles are swapped and the new driver makes it pass and writes the next failing unit test. Then, roles are swapped again and so on and so forth.

Apart from roles, make sure to switch pairs frequently. In case the whole team is pairing amongst themselves, perhaps it could be a daily scrum discussion. I've heard of team, which pair by default, that apply a soft and hard swaps a couple of times throughout the week. So, for instance, every Monday, there is a *soft swap* and people are free to either continue pairing with their colleague or swap to work on another task or with someone else and every Wednesday there is a *hard swap*, in which people actually have to switch pairs. No matter which method you use, I would suggest making sure that pairs are rotated frequently.

Arguably, the best results out of pair programming come when people of the same level and expertise work together (for instance novice - novice or expert - expert). However, I would encourage you to also try mixing it up a bit and have expert - novice pairs. In this case, pay extra attention to not having the expert driving a lot! If anything, make sure that the novice is driving more, otherwise, you may end up with the novice *watching* the expert programming and getting lost and giving up soon. Also, an expert may be particularly unwilling to pair with a novice, believing that it will slow her down, and it will, but always remember that

> Pair programming may slow the expert down for a few hours, but it will speed the novice up for the rest of her life

* Suitable desk - both should have equal access
* Two keyboards
* Frequently switch drivers
* Rotate pairs within the team
* Prefer same level, but also try expert - novice (but avoid having the expert driving a lot)

# When

As I mentioned above, there are teams out there that pair by default. However, I personally feel that there

When Tackling a very difficult problem or a mission critical task, try to pair. The quality of the code will rise, the number of defects will drop and, - arguably - most importantly, it will create collective code ownership.

* Tackling a difficult problem (mission critical tasks)
* Making architecture and design decisions

While knowing when it to pair is important, we should also know when *not* to pair.

* Not pair when solving trivial tasks

# For how much

Of course, as with most practices, pair programming is not a silver bullet and we should be cautious when or for how much we practice it.

Something to always keep in mind is that writing code in pairs is *exhausting*. It requires a tremendous level of concentration, exactly like individual programming, plus a lot of energy devoted to interacting with your partner. After a few hours of pairing, it grows increasingly harder to keep producing high-quality work, which is the goal after all. So, *empirically*, I believe that it is wise to practice pair programming for only a few hours per day. Of course, how many "few" actually is varies among teams and I strongly suggest that each team (or pair) experiments and - empirically - finds its own balance, that works best for it.

If you do practice pair programming though, I would suggest that you do it on a frequent basis, every day if possible.

# Remotely

A question that always comes up refers to team working remotely. Remote work is an integral part of software engineering teams and...

# Challenges

* Sceptics (uncomfortable, afraid of lower efficiency)
* The pair should be engaged (the observer should be playing an active part too)
* Embrace communication throughout the task

# Consider Mob

# Conclusion
