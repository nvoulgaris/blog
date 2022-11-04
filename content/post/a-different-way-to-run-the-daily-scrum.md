---
title: "A different way to run the daily scrum"
date: "2022-11-04"
tags: [agile,scrum]
image: img/posts/a_different_way_to_run_the_daily_scrum.jpg
---

I decided to write this blog post, in order to challenge the formalistic way in which the daily scrum is often run and share an alternative format for it. I have been using this format for over 3 years now. I had to find myself as a new team member to an existing team to notice how useful it has been and to remember that it is not the default way to go.

Our daily scrum was exhibiting some dysfunctional symptoms back then and we decided to adopt this approach as an experiment. It turned out so successful that we never changed it - although we tweaked it a few times. Today, I don't remember if this technique was based on something I read at the time or not. Feel free to point me to any references that deserve credit in the comments section.

# Symptoms

Before changing anything, we have to learn to identify the cases that call for change. For this purpose, I have listed some symptoms that I find to be good indicators. Let's go over them.

## No collaboration

During the daily scrum, team members share their input, but no fruitful communication takes place. To better understand this, let's think of the following hypothetical daily scrum situations:

 * **Situation #1**: *Mark*: "Yesterday, I finished the implementation and  opened a PR for this PBI. Today, I will start work on this one until I get some review feedback".

 * **Situation #2**: *Mark*: "Yesterday, I finished the implementation and  opened a PR for this PBI. Can somebody review it?" *Helen*: "I would, but I have lots of meetings today. I will be able to review it tomorrow though." *Jason*: "I can do it. Let's just make sure to upload it in a dev environment too." *Mark*: "Thanks guys. I'll upload it and then I'll work on this PBI until I hear back from you."

 Mark is sharing the exact same input in both cases, but notice how the work progresses in the second situation. In the first case, the team is not collaborating.

## Monologue

As mentioned above, the daily scrum is all about collaboration. If people are only speaking when their turn is up, how are they collaborating? Instead, a healthy team should be syncing and planning during the session. We should be hearing things like "Shall I use the dev environment to test this?", "I will release after the scrum. Do you want me to wait for this to be merged?", "Shall I branch off your branch on this on  or from develop?", "Do you need any help with this or shall I pick something up from the ToDos?".

People not being fully engaged, being indifferent and *only talking when their turn is up* is a sign that clearly shows that the session is dysfunctional.

## No planning ahead

The daily scrum is supposed to be a *planning session*. Not a reporting session. Yes, we share the latest developments, but we do so in order to *plan the next 24 hours*. Try to keep track of the planning/reporting ratio. If it decreases, it is a very bad sign. Of course, this cannot be measured, but keep an eye on it and it will be easy to see the trend.

## Stuck PBIs

In scrum, we are supposed to be delivering value fast. It doesn't make sense to have a bunch of PBIs stuck at the "Review" swimlane for 3 days and picking up new work instead of reviewing the open PRs. The daily scrum is the time and place to make these decisions if they are not made during the day.

Bottlenecks in the sprint board can be an indication of poor daily scrums. Of course, the root cause may be different here, but when we see jammed swimlanes we should think of the daily scrum.

## My PBI

Often you may hear people use phrases like "Yesterday, I finished the implementation in my PBI". This is a highly problematic situation, as this single phrase implies that the team members are not thinking of the sprint's work in a collective way. They work isolated and this can impede their understanding of success. Completing *"my"* PBI while my teammate struggles doesn't make sprint a success. This doesn't mean that the team members are selfish. All I am trying to say is that software engineering is a team sport and it takes effort to deeply understand this and change your day-to-day work habits accordingly.

# Another way

The typical format most teams that I know of use is the "What did I do yesterday? What will I do today? Do I have any impediments?". I usually call this the "per-person" format. However, remember that the format is up to the team to decide. Consulting the scrum guide we find the following:

> The Developers can select whatever structure and techniques they want, as long as their Daily Scrum focuses on progress toward the Sprint Goal and produces an actionable plan for the next day of work.

## Overview

 An alternative to the "per-person" format would be a "per-PBI" format. With this approach, the team works the spring board top to bottom and right to left. Every open PBI is discussed and the focus is on what the team needs to do in the next 24 hours to move this PBI towards the right ("Done" swimlane).

Let's use an example to understand it better. Assuming that the team's sprint backlog is the following:

{{< figure src="/img/posts/sprint_board.png" alt="Figure 1.1: Sprint board" >}}

The daily scrum would first focus on the topmost PBI in the "Delivered" swimlane. They would ask if it can be considered done. If yes, it would be moved to the "Done" swimlane. If not, a team member could undertake to check if it works as expected and move it to "Done". Then they would do the same for the second "Delivered" PBI if there was any and so on and so forth.

Then they would move to the "Merged" swimlane, focusing on how could they get these tickets to "Delivered". Would they deploy on production? If yes, who would undertake it? Are there any dependencies that need to be deployed as well? Who should be notified? These are the things that *should* be discussed during a healthy daily scrum.

The next step would be the "Review" swimlane, in which the team needs to ensure that the PBIs do not remain idle for review if there is the capacity from team members to review them. They could decide who gets to review what and share more context if needed. Priorities could be defined if time/capacity does not suffice for all the PBIs. Again, the focus would be on how to get these PBI to "Merged" within the next 24 hours.

Then, they would briefly discuss the "In Progress" PBI, sharing progress, impediments and making clarifications if needed.

Finally, there can be some time to share anything that needs to be shared and wasn't already covered.

## Advantages

### Reduced lead time

This format focuses on getting things done and delivering value. It's all about what needs to be done within the next 24 hours to move this PBI to the next swimlane. Inevitably, this prioritizes closing the open PBIs over opening new ones. As we have already discussed in the [*Limiting work in progress*](https://nvoulgaris.com/limiting-work-in-progress-in-scrum) post, this reduces the team's lead time.

### Teamwork mentality

Furthermore, the transition from monologue to an intensely collaborative format builds stronger team relationships and fosters the teamwork mentality. The team learn to function as a unit, as opposed to a set of individuals. They learn to cooperate and they understand that great results take more than an individual writing code. There is no "my PBI" anymore. There is "our work".

## Considerations

### Longer daily scrums

From my personal experience, I've noticed that the session sometimes tends to last longer with this format. This is a direct result of the dialogue that it fosters. There can be a number of reasons why this is. The first thing that should come into our minds is whether there are too many open PBIs. If yes, the team should focus on closing some of them before starting to work on new ones. It could also show that the team is getting dragged into long conversations, which could be kept shorter. Finally, maybe the team *needs* this extra time. Personally, I wouldn't mind a slightly longer daily scrum so long as the conversation is fruitful and meaningful.

### People feel left out

Additionally, people whose work is not directly visible on the board (e.g. designers and product owners) could start to feel left out with this format. My advice would be to encourage them to contribute whenever needed in the conversation and to use the time at the end of the session to share their input if it wasn't already shared.

# Own the process

Having shared this technique, which I have successfully used, it is important to understand that **every team is different**. Just because it worked for a team it doesn't mean that it will also work for another one. Dogmatically applying a solution that worked for another team and expecting results goes against the very nature of the agile mindset. I would not advise against applying this format, but rather use it as a starting point. Call it an experiment and remember to evaluate this experiment. Then tweak it and run another experiment. Evaluate this one too. Then tweak it again. Chances are that the result that works for your team is different than the one I described. Maybe slightly different, maybe radically different. The point is to understand that the **process is here to serve us** and not the other way around. If it is not working, then change it to something that works. Make it your own.

# Conclusion

The daily scrum is a pivotal event that can make all the difference between a successful and a failed sprint. Often, it gets executed in a formalistic way, which offers no real value. There are a number of symptoms that can help us identify a dysfunctional daily scrum session, such as lack of planning for the next 24 hours, jammed swimlanes and people not engaging in conversation during the session.

A different way to run the session can prove beneficial. I have successfully used what I call the "per-PBI" format to run daily scrums and I feel that it offers a series of advantages, such as reduced lead time and improved team cohesion. Along with it, of course, come some downsides, such as certain roles feeling left out and increased duration of the session.

No matter if we choose the "per-PBI" format or not, the responsibility of identifying the dysfunction and taking action to improve the situation lies with us, the software engineering team. So, I would strongly advise for experimenting with different formats and tweaking the process until it serves the team
