---
title: "Limiting work in progress in scrum"
date: "2020-05-03"
tags: [agile, scrum]
image: img/posts/wip_limits.jpg
---

# Symptoms

Let's imagine a scrum team consisting of five software engineers is in the middle of a two-week sprint. The first five stories *in-progress* and the team is juggling among them, trying to advance all of them at the same time.

There is a number of issues that one could note in the above-mentioned situation. I would argue that the first one is the **lack of focus**. Focus is one of the five Scrum values. It is a quality that without it, scrum can never work. It is as simple as that. Although the team is focused on a macro-level (there is a two-week sprint with a well-defined sprint goal), the lack of focus on a micro-level is resounding.

Secondly, there is a **total absence of priority**. A sprint board is sorted in a particular way, based on the priority of the stories. The higher the priority of the story, the higher on the board the story is. Trying to put this priority in words, it would be something as follows: *"if as a team we manage to get a single story done in the sprint, let this be the topmost one. If we get two stories done, let them be the first two ones"* and so on and so forth. A team that is working on five stories in parallel does not honour the notion of priority and to some extent, it is missing part of the essence of *Scrum* as a framework.

Furthermore, a team in such a situation exhibits **chemistry issues**. Perhaps people do not enjoy working with each other or they believe that it is not efficient. Whatever the reason, there is no teamwork (e.g. pair programming) and the team is behaving like a set of individuals instead. However, great results are more often than not delivered by great *teams*.

Such a workflow has the tendency to lead to a **big bang release** towards the end of the sprint. This allows for no time to react to a release that caused issues and it does not give a smooth, steady flow of value to the stakeholders and the users. A failed release could cause the sprint to fail.

Lastly, this way of working inevitably leads to significantly **small [bus factors](https://en.wikipedia.org/wiki/Bus_factor)**, usually to a bus factor of one or two. This impedes collective code ownership and in case an individual leaves the team, a knowledge gap is also created.

I could continue commenting on this situation, but I believe that I have made my point. So, (hopefully) agreeing that this is a problematic situation, let's go over a technique that can mitigate it.

# What is a WIP limit

Limiting work-in-progress is a very simple technique.

> A WIP limit is a number indicating the maximum items (e.g. stories, tasks) tha may be in-progress at any given moment.

So, if a team has a WIP limit of two stories, it can only work on two stories at the same time at any given moment. In order to start working on a third one, one of the two previously in-progress has to be *done*.

It originates from Kanban and there it applies to tasks on the team's Kanban board. In Scrum, it can either be applied to stories or story tasks, depending on what works best for the team.

## Can this be applied to scrum?

It would be reasonable to wonder whether there would be any sense in applying such a technique to Scrum, given that the work is bound by the sprint duration. One could argue that WIP limits in Kanban make sense because there is no such boundary.

However, considering all the above-mentioned symptoms, which could be more or less addressed by applying a WIP limit, I feel that it is meaningful. As a matter of fact, we have applied it in teams that I have been a part of with considerable success.

In case applying a Kanban technique to Scrum feels like breaking the rules, let's always keep in mind that being *Agile* is all about the **culture**. Blindly adopting a set of rules is a cargo cult mentality that leads nowhere. If you ask me, if WIP limits serve us, let's use them.

# WIP limit benefits

Let's examine some of the benefits that a team would expect by applying WIP limits.

## Reduced lead time

*Lead time* is a metric, expressing the time elapsed between starting and completing an item of work.

> A scrum team's lead time is the time required between the team committing to a story (sprint planning) and the story being *done*.

Let's study again the hypothetical example of the scrum team of five software engineers in the middle of the sprint with five stories in-progress. Let's also assume that the team manages to complete all five stories at the very last day of the sprint and that these were all the stories in this sprint. What is the lead time of the team?

Each of the five stories took nine days (the working days of a two-week sprint excluding the scrum events day) to complete, so the team's average lead time is

> (5 * 9) / 5 = 9 days

Let's assume that the team had applied a WIP limit of two. This means that no more than two stories could be worked on parallel. The first two stories could perhaps be *done* in the third and fourth day respectively. The next two stories could be completed in the seventh and eight days respectively and the last story could be completed on the very last day of the sprint. Let's calculate again the team's average lead time.

> (3 + 4 + 7 + 8 + 9) 5 = 5.4 days

These numbers are fictitious up of course, but they are meant to illustrate the point. As a matter of fact, feel free to fiddle with the numbers and inspect the results. The will always be less than nine and I feel that plugging some reasonable numbers in the formula, will result in an average lead time significantly below 9, like 5.4.

This essentially means that the team delivered value early. The stakeholders and product users had increments on the third and fourth day instead of the ninth.

## Teamwork

## Bus factor

## Identify bottlenecks

# Fine-tuning the limits

## Avoid multitasking

## Not too high

## But not too low either

## Inspect and adapt

# Conclusion