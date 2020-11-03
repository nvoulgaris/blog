---
title: "Agile theater"
date: "2020-10-18"
tags: [agile]
image: img/posts/agile_theater.jpg
---

Almost 20 years past the authorship and signature of the Agile manifesto and the true message that these original thinkers tried to send has gone astray. The residual believers of the original ideas of the Agile manifesto have found shelter in the Software Craftsmanship movement, but nowadays the roots of the problem lie far deeper than the lost ideas and the wasted potential to do things better.

The misinterpretation of the philosophy of the agile manifesto combined with the creation of a number of frameworks, certifications and job titles has resulted in a chaotic situation. A situation which not only faces the exact same problems that led to the creation of the Agile manifesto in the first place, but which increases complexity and adds more work to be done by people who dogmatically follow some obscure guidelines which they do not understand in the first place.

If you are part of an agile organization, have you ever taken a step back to create distance between yourself and your work and reflected on how you do things in your organization? Is this better than the waterfall approach? If yes, why is it so? What adds *true value*? What has improved and in what way?

These questions should be easy to answer, especially by anyone who is part of an organization that has spent enormous amounts of effort and money in a so-called agile transformation and yet, they prove astonishingly difficult. In this blog post, I will try to put in words what *I believe* the true Agile mindset is.

# The problem

As with most problems, before attempting to provide a solution, one has to really understand the problem. So, let's try to delve into it. Let's study the following, hypothetical case.

A company decides to become Agile and use Scrum. An Agile coach is hired and the so-called Agile transformation begins. The offices are rearranged, new shiny boards are installed and Scrum Master and Product Owner roles are born and filled. Every two weeks a new iteration begins, the goal of which is a chunk of the promised-to-the-client release in a few months time. People stand up for no more than 15 minutes a day, discussing their progress and coordinating and the walls are full of sticky notes describing tasks. The software engineers still write code in the exact same way they did before, but now in 2-week iterations. No other department has changed the way it works, apart from the engineering department.

Now, I repeat that this is a hypothetical scenario, but to the extent of my knowledge, a very realistic and typical one. This *"transformation"* is doomed to fail. It is precisely this kind of *"transformations"* that have caused a lot of people to lose faith in the Agile way of working. This approach is fundamentally flawed. It completely misses the essence and, at the end of the day, defeats the purpose. Situations like these are commonly described by the term *Agile theater*.

Let's examine what's wrong with that approach. The core idea of the Agile mindset is that

> the people who need the software (stakeholders/users) collaborate closely with the people who make the software and they are able to adjust the course as often as needed

We will discuss thoroughly how this may be achieved later on, but first, let's understand why the above-mentioned changes do not serve this goal.

 * Releases are planned and promised to the customer with certain deadlines. This does not allow for *adjusting the course*. The work is still treated in a *waterfall* approach. The software engineering department initiative of breaking the release work down to 2-week chunks *offers nothing* without the rest of the stakeholders and the customer actively participating in that 2-week loop.

 * The software engineers have *changed nothing* in the way they write code. Even if the stakeholders and the customer were actively engaged in the loop and even if the course *was* adjusted every two weeks or so, how could the software engineers respond to that? If you were to take one thing away from this post, let it be the following: **Changing the process means nothing without changing the way code is written**


# Feedback loops

A truly agile way of working requires constant adaptations. Constant adaptations require a constant flow of feedback. Therefore, lots of feedback loops should be created. The shorter these loops are the more adaptation they will allow for. The sooner one receives feedback on one's action, the easier it is to amend mistakes.

A feedback loop may sound like a subtle concept, but if you think about it, it's everywhere in our work:

 * Scrum events are feedback loops. During the daily scrum, the team receives the feedback of yesterday's work and adaptst to it for the upcoming day. During the sprint retrospective the team collects the feedack of the way they worked in the previous sprint and makes amendments for the upcoming sprint. During the sprint review the stakeholders generate feedback on the completed increment and the product backlog get adjusted based on it (*sprint review is so misunderstood that perhaps deserves a blog post of its own*).

 * Test Driven Development is a feedback loop. A very short one actualy (when done right). The engineers set up a loop between the code and themselves. A change in the code produces immediate feedback. Did the change work? Did it break anything? Does the code written in the last few seconds need modifications? *This actually constitutes the fastest feedback a software engineer will ever get on her code.*

 * Pair programming is a feedback loop. This loop is set up between the two engineers working together. The code one writes produces feedback from the other, which changes the code, which changes the feedback and so on and so forth.

 * Code reviews are a feedback loop. Actually, it is the exact same loop with pair programming, except that it involves more people and the feedback flows *significantly slower*.

# Enabling inspection and adaptation

Returning to the original idea of adjusting our course as often as needed based on feedback, I believe it is becoming aparent that feedback loops enable organizations to align with it.

# Scaffolding

Now let's assume that we could do all these things. We could flip the magic switch and, starting from tomorrow, we could create more feedback loops, shorten them, use the feedback and adapt based on it, embrace all XP technical practises etc. 

Why would it make sense to use an Agile framework then? Changes create discomfort. It's natural. Especially when they are radical and they concern the way we work every day. What would scrum, kanban, SAFe, LeSS, you-name-it provide that would justify this tremendous effort and energy needed to adopt them? Take a minute to reflect before proceeding.

My answer would be a resounding *nothing*. If we already enjoy all the merits that these frameworks bring, why bother adopting them?

However, this magic switch does not exist. That's were the frameworks come into play. They could be used to *initiate* the transition and help us create all these good habits. They would work us our guidance. They would essentially be *scaffolding* to the whole shift of mindset.

If we apply them in a ritualistic way, we remain oblivious to the true merits that they can bring along and we end up being slaves to 

# If it's the same for everyone, it's not agile
