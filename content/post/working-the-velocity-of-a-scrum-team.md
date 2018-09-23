---
title: "Working the velocity of a scrum team"
date: "2018-09-23"
tags: [agile,scrum]
image: img/posts/velocity.jpg
---

Scrum has gone wrong in a number of ways. This is a fact. Agile, an initiative born by software engineers, has turn into a new, *cool* product management way. A considerable number of companies advertise that they use scrum when all they do is run a standing, 15-minute meeting in the morning and use sticky notes, being totally oblivious the true mindset of the framework as well as the immense benefits that it can provide.

Among a lot of factors that have resulted to this, arguably the king of the problems is how people misunderstand the concept of the *velocity* of a scrum team. Scrum Masters and Product Owners treat it as a productivity reporting tool, trying to make the development team *commit* (we will discuss this *"commitment"* issue in another post) to as high a number as possible, while the development team, feeling that they are judged by this number, struggle to increase it sprint by sprint. However, this is a **fundamentally flawed** view.

> Velocity is not a productivity reporting tool!

I wish I could stress this even more. **Velocity is not a productivity reporting tool!**.

Since I - once again - started with what velocity *is not*, let's proceed in a more conventional way and talk about what velocity actually *is*.

# Inspect and adapt

Let's try to go back to the basics and essence of Scrum for a bit. In a nutshell, every couple of weeks (in reality this number ranges between 1 and 4 weeks, but for simplicity's sake I will use 2 weeks for a sprint's length throughout this post) the scrum team gathers with the stakeholders, reviewing their latest increment, inspecting the state of the product and refining the priorities. After this comes the retro and after the retro, the new spring begins with a sprint planning session: the most important meeting in scrum.

Now the scrum team should take into consideration the outcome of the sprint review and retrospective in order to commit to a new sprint. A new sprint, which should accommodate the prioritized requirements of the product, as defined by the stakeholders, whose voice in this meeting is the Product Owner. Let's think of this for a moment. How is the scrum team supposed to commit to a couple of week's worth of work without having an **estimate** on the amount of work they can deliver in this time?

# Sprint planning

In order to execute a sprint planning session meaningfully, there have to be two inputs: a **refined Product Backlog** and the team's calculated **velocity** for the upcoming sprint. These will produce a single output: a **sprint backlog**. The Scrum Master should see to this.

Now it is becoming visible that the team's velocity is *key* to deciding on how many and which Product Backlog Items should the scrum team work on the upcoming sprint. This is an *indication*, which the team should *consult* when asking questions like *"is this amount of work a reasonable chunk for the upcoming sprint? Is it too much? Should we work on more items"*.

If it is reasonable for one to assume that the team is able to successfully work on more items than they actually put in the sprint backlog, then the team is **undercommitting** and therefore failing to honor their role as *professional* software engineers. If the team is clearly committing on a sprint that will most likely fail to deliver, it is **overcommitting**, failing once again to honor their role as *professional* software engineers, as they create expectations for the stakeholders that they will not be met.

This is exactly why velocity is **critical** to the success of a sprint planning session and therefore to the success of the sprint. **Velocity helps creating a sustainable pace**. This pace will neither burn the team out or leave it idle for too much. Additionally, it provides *confidence* to the development team to estimate their upcoming work in *reasonable chunks*. Chunks that they can actually deliver, therefore causing the *trust* of the stakeholders in the development team to increase.

# Calculating the team's velocity

Now, having said all these, I hope that it is clear that monitoring the team's velocity is very very important, but *who* actually is responsible for this and *how* can one do a good job on it? After all, no one can predict the future and the work that a group of people will produce in two weeks time seems quite hard to get right.

## Who

### The Scrum Master's role

The Scrum Master is sometimes called the *joker* and part of the reason is that she has a lot of balls in the air at any given moment. One of these is that she is responsible for monitoring the team's velocity and coming up with reasonable calculations for upcoming sprints as input in the sprint planning sessions.

### Who else needs to know

I once was working in a company that used to start the sprint reviews with the following phrase: "Our estimated velocity for the past sprint was ... and our actual velocity was ...". I **completely disagree** with this (I had stated it a number of times)! Velocity is a piece of information that, in my opinion, concerns solely the scrum team members (perhaps excluding very few cases).

The stakeholders definitely need **not** know the velocity of the team. They only need to know that the team is maturing and *can be trusted* in their estimates. Otherwise, this would only enforce the view that the development team's productivity is being judged by their velocity (at least in their eyes).

The Product Owner should learn the calculated number by the scrum master for the sprint planning purposes, but should not be concerned thereafter.

The development team should learn the calculated number by the scrum master for the sprint planning purposes, but should not be concerned thereafter either.

## How

Estimating the velocity of a scrum team for the upcoming sprint is not a straightforward task. Estimation by itself is not an easy task anyway. Needless to say, there is no silver bullet for it. But the good news is that there doesn't have to be one. We're not after a precise, infallible estimation. We're after creating rhythm, building confidence and trust.

A number of techniques are being daily applied by different Scrum Masters in different teams. None is right. None is wrong. Let me try to describe a technique that I have used for quite a long time and I find it useful.

### One technique

In the heart of the technique lie statistical calculations based on empirical data. A number of factors that affect the estimated velocity, are literally plugged into an formula that produces the magic number. The factors are listed and explained below:

* **Team members**: The number of members of the development team. Do not confuse this with the number of members of the scrum team, which will be different if either the Scrum Master or the Product Owner do not contribute to writing code.
* **Sprint duration**: The days which will be available for the scrum team to complete its work in the sprint. Personally, I do not include the day of the scrum events, as no code is written during this day.
* **No workdays**: Days during which the team will not be working during the sprint (e.g. bank holidays, conferences that the whole team attends etc)
* **Team holidays**: Days during a single team member will not contribute to the team's work (e.g. annual leave). For instance, if a member has submitted annual leave for a day and another member for two days, this number will be 3.
* **Focus factor**: A number indicating how reliable the team's commitments tend to be. I explain this factor in depth further on.

**Actual work days** is produced by the following formula:

> (Team members * Sprint duration) - (Team members * No workdays) - Team holidays

**Focus factor** is a bit more complicated. Basically, the piece of information that we want to take into consideration is the degree in which the team estimations match the actual work done. The reason for using more than one past sprints is that as teams change, as they mature they go through different phases. These affect their focus factor. For instance, as a new team member is integrated with the team, one would expect the focus factor to have an slightly increasing trend. The focus factor for a single sprint is provided by the following formula:

> Actual velocity points / committed velocity points

Finally, the formula producing the estimated velocity for the upcoming sprint is the following:

> (Actual work days) * (average focus factor of the last x sprints)

* *I usually use the average focus factor of the last 3 sprints (x = 3), but feel free to use any number of sprints that works for you*

* *I find it very convenient to use an excel spreadsheet for these calculations. I just plug the numbers in every sprint and I have both the calculations ready and reliable metrics and statistics when I need them. (I have a template for this spreadsheet. Do not hesitate to ask me for it. I will gladly share it.)*

* *Never forget that this number is a statistical calculation. Reality is much more complex. So, before committing to a sprint backlog, __always__ make sure that the team believes that this is a reasonable chunk of work for the upcoming sprint. Ask them to forget about the number and actually do a gut feel. Don't just blindly follow the output of any formula or technique.*

Probably a couple of very reasonable questions have already formed into your mind, like *"What do we do on the first sprint, with no previous data existing yet?"* or *"What if a new member joins the team?"*. Let's discuss these both.

### First sprint

A very challenging period to estimate a team's velocity is right after the team is formed. After all, there are no previous data whatsoever. There is no silver bullet for this problem either, but I would propose the following method: make sure that for the first few sprints the team bluntly **overcommits**. Not slightly overcommitting, but estimate a profoundly unreasonable amount of work. Explain to the team that this is happening for precise reasons and no one is expecting them to deliver this mountain of work. Protect them from destroying their morale! Now, over the first sprints (I believe roughly 3 will suffice), the current ability of the team will become clear. When confident, stop this and use a proper method for calculating the velocity, like the one described above.

### New team member

A usually confusing case is when a new software engineer joins the development team. Intuition suggests that the team's velocity should increase. After all, there is one more engineer now, right? This is true, but in the long term. On the contrary, over the first few sprints, it is more likely that velocity will drop. Obviously, the new engineer, no matter how skillful, is not going to be productive right away. To make matters worse, the current engineers will have to both spend time on her orientation and keep on carrying out their regular work. This leaves them with less time to do the latter. Therefore, the most likely scenario is that velocity will drop slightly for the first few sprints and then gradually catch up and probably exceed the previous numbers (of course this also depends on how the new team will glue together, but this is another post).

# Conclusion

Perceiving velocity as a productivity reporting tool is **flat out wrong**. Productivity is measured indeed, but not for reporting. Just for internal use within the team. Use it to create a sustainable pace, to help the team deliver on a steady basis, create trust and mature the team. The actual method for calculating the velocity for upcoming sprints does not matter. There are loads of techniques out there. Either pick one or create your own. Just make sure that you use it in the right way and it helps the team.
