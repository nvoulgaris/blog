+++
title = "Limiting work in progress in scrum"
date = "2020-05-17"
tags = ["agile","scrum"]
image = "img/posts/wip_limits.jpg"
description = "Experimenting with Kanban's WIP limits to elevate a scrum team"
+++

How would you identify bottlenecks in your team's process? How would you surface them? How would you encourage the team to increase collaboration? How would you decrease lead times and increase the bus factor?

Working in an *Agile* way is far from following a predefined set of rules. On the contrary, is all about *inspecting and adapting*. It's about finding what works best for the team and it is an *ever-ending* process. This includes a lot of *experimentation*. Adopting something new for a few days/weeks, evaluating its benefits and either keep it or discard it before you move on to the next experiment. A team not chasing continuous improvement cannot be *Agile*.

This post is all about experimenting with limiting work-in-progress (WIP). Applying WIP limits is a beautiful technique, originated in Kanban, but I believe it can be applied very effectively on *Scrum* teams too. Before we analyze the technique though, let's briefly go over the symptoms that may push a team towards experimenting with WIP limits in the first place.

## Symptoms

Let's imagine a *Scrum* team consisting of five software engineers is in the middle of a two-week sprint. The first five stories *in-progress* and the team is juggling among them, trying to advance all of them at the same time.

There is a number of issues that one could note in the above-mentioned situation. I would argue that the first one is the **lack of focus**. Focus is one of the five *Scrum* values. It is a quality that without it, *Scrum* can never work. It is as simple as that. Although the team is focused on a macro-level (there is a two-week sprint with a well-defined sprint goal), the lack of focus on a micro-level is resounding.

Secondly, there is a **total absence of priority**. The stories in a sprint board are sorted based on their priority. The higher the priority of the story, the higher on the board the story is. Trying to put this priority in words, it would be something in the following lines: *"if as a team we manage to get a single story done in the sprint, let this be the topmost one. If we get two stories done, let them be the first two ones"* and so on and so forth. A team that is working on five stories in parallel does not honour the notion of priority and to some extent, it is missing part of the essence of *Scrum* as a framework.

Furthermore, a team in such a situation exhibits **chemistry issues**. Perhaps people do not enjoy working with each other or they believe that it is not efficient. Whatever the reason, there is no teamwork (e.g. pair programming) and the team is behaving like a set of individuals instead. However, great results are more often than not delivered by great *teams*.

Such a workflow has the tendency to lead to a **big bang release** towards the end of the sprint. This allows for no time to react to a release that caused issues and it does not give a smooth, steady flow of value to the stakeholders and the users. A failed release could cause the sprint to fail.

Lastly, this way of working inevitably leads to significantly **small [bus factors](https://en.wikipedia.org/wiki/Bus_factor)**, usually to a bus factor of one or two. This impedes collective code ownership and in case an individual leaves the team, a knowledge gap is also created.

I could continue commenting on this situation, but I believe that I have made my point. So, (hopefully) agreeing that this is a problematic situation, let's go over a technique that can mitigate it.

## What is a WIP limit

Limiting work-in-progress is a very simple technique.

> A WIP limit is a number indicating the maximum items (e.g. stories, tasks) tha may be in-progress at any given moment.

So, if a team has a WIP limit of two stories, it can only work on two stories at the same time at any given moment. In order to start working on a third one, one of the two previously *in-progress* has to be *done*.

It originates from Kanban and there it applies to tasks on the team's Kanban board. In *Scrum*, it can either be applied to stories or story tasks, depending on what works best for the team. Also, the very definition of *in-progress* may be adjusted according to the team's needs. For instance, a story can be considered *in-progress* until it is code-reviewed or until it is deployed to production. The limits may span on a number of different swimlanes as well and each swimlane can have its own limit.

### Can this be applied to scrum?

It would be reasonable to wonder whether there would be any sense in applying such a technique to *Scrum*, given that the work is bound by the sprint duration. One could argue that WIP limits in Kanban make sense because there is no such boundary.

However, considering all the above-mentioned symptoms, which could be more or less addressed by applying a WIP limit, I feel that it is meaningful. As a matter of fact, we have applied it in teams that I have been a part of with considerable success.

In case applying a Kanban technique to *Scrum* feels like breaking the rules, let's always keep in mind that being *Agile* is all about the **culture**. Blindly adopting a set of rules is a cargo cult mentality that leads nowhere. If you ask me, if WIP limits serve us, let's use them.

## WIP limit benefits

Let's examine some of the benefits that a team would expect by applying WIP limits.

### Reduced lead time

*Lead time* is a metric, expressing the time elapsed between starting and completing an item of work.

> A *Scrum* team's lead time is the time required between the team committing to a story (sprint planning) and the story being *done*.

Let's study again the hypothetical example of the *Scrum* team of five software engineers in the middle of the sprint with five stories in-progress. Let's also assume that the team manages to complete all five stories at the very last day of the sprint and that these were all the stories in this sprint. What is the lead time of the team?

Each of the five stories took nine days (the working days of a two-week sprint excluding the *Scrum* events day) to complete, so the team's average lead time is

> (5 * 9) / 5 = 9 days

Let's assume that the team had applied a WIP limit of two. This means that no more than two stories could be worked on parallel. The first two stories could perhaps be *done* in the third and fourth day respectively. The next two stories could be completed in the seventh and eight days respectively and the last story could be completed on the very last day of the sprint. Let's calculate again the team's average lead time.

> (3 + 4 + 7 + 8 + 9) 5 = 5.4 days

These numbers are fictitious of course, but they are meant to illustrate the point. As a matter of fact, feel free to fiddle with the numbers and inspect the results. The result will always be less than nine. I feel that plugging some reasonable numbers in the formula will result in an average lead time *significantly below* 9, like 5.4.

This essentially means that the team delivered value early. The stakeholders and product users started having increments on the third and fourth day of the sprint instead of the ninth.

### Teamwork

A WIP limit is essentially the application of a restriction. A restriction on the amount of work that can be concurrently undertaken. However, team members remain the same despite the restriction. Hence, the smaller the number of stories or tasks that can be simultaneously *in-progress* the more the level of cooperation among the team members has to increase.

Think about it. In a very simplistic scenario, a team of two software engineers with a WIP limit of one would always pair (in the case where the WIP limit is applied to tasks) or - at least - work on the same story (in the case where the WIP limit is applied to stories). A team of - say - 5 software engineers with a WIP limit of four would mean that there should always be at least one pair. Reduce this to a WIP limit of three and the pairs become at 2 at all given moments.

Pairing is a more intense form of collaboration, but working on the same story is still more collaborative than two software engineers working on different stories. Given sufficient time, this restriction will strengthen the team bonds and will help build the right chemistry.

### Bus factor

Increased teamwork goes hand in hand with increased bus factors. I believe this is quite straightforward. The more often two or more people work on the same story, the more the parts of the code that more people will be familiar with. On the contrary, a team whose members tend to work alone on a story will end up with a codebase full of parts that only a single software engineer is familiar with.

### Identify bottlenecks

Applying a WIP limit is a tailor-made technique for surfacing bottlenecks in a team's process. Let's imagine a scenario in which a team uses the flow *"todo"*, *"doing"*, *"review"*, *"delivered"* and then *"done"*. It undertakes stories and when the code is written, the story is passed to the rest of the team for code review. The engineer(s) that worked on this story naturally grab the next one until this one gets reviewed. It is quite common for teams to end up with a pile of stories that should get reviewed towards the end of the sprint. This, of course, leads to rushed code reviews and a big bang release with a dozen features in it. This is a typical case of a *bottleneck in the process*.

Now, let's imagine that this team applies some WIP limits. Remember that these may span from one to several swimlanes. Let's assume that the *"review"* swimlane has a dedicated limit of three stories. When the third story gets in the lane the team should prioritize code reviewing these stories. Otherwise, no new stories can be propagated from *"doing"* to *"review"*. These stories will be reviewed and if the *"delivered"* column has a respective limit, they will also get deployed to production and eventually reach *"done"*, allowing space for more stories to be worked.

The application of the limit has not only made the problem apparent, but it has also provided a solution to it.

## Fine-tuning the limits

Assuming that some symptoms are visible and the team feels that some WIP limits would be helpful, a natural question would be how can a team go about setting them. What are the right the numbers? How many swimlanes should a limit span?

### Avoid multitasking

I would propose that the first thing to avoid is multitasking. A WIP limit greater than the number of software engineers in the team would mean that people are encouraged to multitask. For instance, imagine a team of five software engineers with a WIP limit of 6.

Keep this in mind. In my opinion, if you are ready to set a WIP limit greater than the number of software engineers in the team, take a step back. Think the problem over again. Why do you want to do this? What do you expect to gain out of it?

### Not too high

Building on this point, a WIP limit equal to the number of software engineers in the team would mean that no one can multitask, but on the other hand, pairing and collaboration are not encouraged. This kind of beats the purpose, because fostering collaboration is a key motive for using this technique.

The two above-mentioned strategies can work but, only as first steps and only in rare situations. For instance, if some team members are very reluctant about using WIP limits and yet the rest of the team feels that they would be beneficial, perhaps it's a decent first step. However, I see very limited benefits besides these cases.

### But not too low either

On the other hand, a very restrictive WIP limit can have negative effects. Not every task and story is suitable for pairing or requires more than one person working on it. Also, pairing is great, but, as discussed in extensively in my [pair programming post](https://nvoulgaris.com/pair-programming-making-the-whole-greater-than-the-sum-of-its-parts/), it can be exhaustive. Setting a WIP limit of two in a team with four software engineers would automatically mean that the engineers should always work in pairs to honour this rule. If this is what you are after - always working in pair - by all means, go for it. However, pay a lot of attention to it. Such a restrictive limit may lead to people feeling that they are suffocating or it may just be counterproductive.

### Inspect and adapt

Having said all these, we still haven't answered the above-mentioned questions. Well, you might have guessed it. There is no *right* answer. *There is no silver bullet*. The very philosophy of *Agile* suggests a totally different approach to *right* answers and *silver bullets*. *Scrum* says *"inspect and adapt"*. That is what I would suggest.

Start off with discussing the situation during the retrospective. Come up with the first iteration of a few WIP limits. Give it a go and watch what happens. Adjust it and repeat the process. This is an ever-ending-process. Keep shifting towards what works best for the team and always keep in mind that different things work on different teams.

## Conclusion

Being *Agile* means being after continuous improvement. This requires being able to read the symptoms and come up with experiments to help the team work better. Lack of focus, disrespect to priority, big bang releases and small bus factors are serious symptoms that should be dealt with.

Limiting work-in-progress can provide a great boost to the team, like reducing the average lead time, improving collaboration, increasing the bus factor, identifying bottlenecks and more. If a team exhibits these symptoms, applying some WIP limits could be an experiment worth considering.
