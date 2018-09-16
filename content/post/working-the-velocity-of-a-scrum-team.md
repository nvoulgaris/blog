---
title: "Working the velocity of a scrum team"
date: "2018-09-11"
tags: [agile,scrum]
image: img/posts/velocity.jpg
---

Scrum has gone wrong in a number of ways. This is a fact. Agile, an initiative that was born by software engineers, has turn into a new, *cool* product management way. A considerable number of companies advertise that they use scrum when all they do is run a standing, 15-minute meeting in the morning, being totally oblivious the true mindset of the framework as well as the immense benefits that it can provide.

Among a lot of factors that have resulted to this, arguably the king of the problems is how people misunderstand the concept of the *velocity* of a scrum team. Scrum Masters and Product Owners treat it as a productivity metric, trying to make the development team *commit* (we will come back to this *"commitment"* issue) to as high a number as possible, while the development team, feeling that they are judged by this number, struggle to increase it sprint by sprint and treat. However, this is a **fundamentally flawed** view.

> Velocity is not a productivity measure!

I wish I could stress this even more. Since I started with what velocity *is not*, let's proceed in a more conventional way, talking about what velocity actually *is*.

# Inspect and adapt

In a nutshell, every couple of weeks (in reality this number ranges between 1 and 4 weeks, but for simplicity I will use 2 weeks for a sprint's length throughout this post) the scrum team gathers with the stakeholders, reviewing their latest increment, inspecting the state of the product and refining the priorities. After this comes the retro and after the retro, the new spring begins with a planning session: the most important meeting in scrum. Now the scrum team should take into consideration the outcome of the sprint review and retrospective in order to commit to a new sprint. A new sprint, which should accommodate the requirements of the product, as defined by the stakeholders, whose voice in this meeting is the Product Owner. Let's think of this for a moment. How is the scrum team supposed to commit to a couple of week's worth of work without having an **estimate** on the amount of work they can deliver in this time?

# Sprint planning

In order to execute a sprint planning session correctly, there have to be two inputs: a **refined Product Backlog** and the **team's velocity**. These will produce a single output: a **sprint backlog**. The Scrum Master should see to this.

Now it is becoming visible that the team's velocity is *key* in deciding on how much Product Backlog Items the scrum team should work on the upcoming sprint. This is an *indication*, which the team should *consult* when asking questions like *"is this amount of work a reasonable chunk for the upcoming sprint? Is it too much? Should we work on more items"*.

If it is reasonable to assume that the team is able to successfully work on more items, then the team is **undercommitting** and therefore failing to honor their role as *professional* software engineers. If the team is clearly committing on a sprint that will most likely fail to deliver, it is **overcommitting**, failing once again to honor their role as *professional* software engineers, as they create expectations for the stakeholders that they will not be met.

This is exactly why velocity is **critical** to the success of a sprint planning session and therefore to the success of the sprint. **Velocity helps creating pace**. This pace provides *confidence* to the development team to estimate their upcoming work in *reasonable chunks*. Chunks that they can actually deliver, therefore causing the *trust* of the stakeholders in the development team to increase.

# Calculating the team's velocity

Now, having said all these, I hope that it is clear that monitoring the team's velocity is very very important, but *who* actually is responsible for this and *how* can she make a good job on it? After all, no one can predict the future and the work that a group of people will produce in two weeks time seems quite hard to get right.

## Who

### The Scrum Master's role

The Scrum Master is sometimes called the *joker* and part of the reason is that she has a lot of balls in the air at any given moment. One of these is that she is responsible for monitoring the team's velocity and coming up with reasonable calculations as input in the sprint planning sessions.

### Who else needs to know

I once was working in a company that used to start the sprint reviews with the following phrase: "Our estimated velocity for the past sprint was ... and our actual velocity was ...". I **completely disagree** with this (I had stated it a number of times)! Velocity is a piece of information that, in my opinion, concerns solely the scrum team members (perhaps excluding very few cases).

The stakeholders definitely need **not** know the velocity of the team. They only need to know that the team is maturing and *can be trusted* in their estimates. Otherwise, this would only enforce the view that the development team's productivity is being judged by their velocity (at least in their eyes).

The Product Owner should learn the calculated number by the scrum master for the sprint planning purposes, but should not be concerned thereafter.

The development team should learn the calculated number by the scrum master for the sprint planning purposes, but should not be concerned thereafter either.

## How

### The technique

### First sprint

A very challenging period to estimate a team's velocity is right after the team is formed. After all, there are no previous data whatsoever. There is no silver bullet for this problem, but I would propose the following method: make sure that for the first few sprints the team bluntly **overcommits**. Not slightly overcommitting, but estimate a profoundly unreasonable amount of work. Explain to the team that this is happening for precise reasons and no one is expecting them to deliver this mountain of work. Protect them from destroying their morale! Now, over the first sprints (I believe roughly 3 will suffice), the current ability of the team will become clear. When confident, stop this and use a proper method for calculating the velocity, like the one described above.

### New team member

A usually confusing case is when a new software engineer joins the development team. Intuition suggests that the team's velocity should increase. After all, there is one more engineer now, right? While this is true, it is so in the long term. On the contrary, over the first few sprints, it is more likely that the velocity will drop. Obviously, the new engineer, no matter how skillful, is not going to be productive right away. To make matters worse, the current engineers will have to spend time on her orientation while keep on carrying out their regular work. This leaves them with less time to do the latter. Therefore, the most likely scenario is that velocity will drop slightly for the first few sprints and then gradually catch up and probably exceed the previous numbers (of course this also depends on how the new team will glue together, but this is another post).

# Conclusion
