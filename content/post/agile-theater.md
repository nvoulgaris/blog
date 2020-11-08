---
title: "Agile theater"
date: "2020-11-08"
tags: [agile]
image: img/posts/agile_theater.jpg
---

Almost 20 years past the authorship and signature of the Agile manifesto and its true message has gone astray. The residual believers of the original ideas of the Agile manifesto have found shelter in the Software Craftsmanship movement, but nowadays the roots of the problem lie far deeper than the lost ideas and the wasted potential to do things better.

The misinterpretation of the philosophy of the agile manifesto combined with the creation of a number of frameworks, certifications and job titles has resulted in a chaotic situation. A situation which not only faces the exact same problems that led to the creation of the Agile manifesto in the first place, but which results in increased complexity and work. This is a direct consequence of people following dogmatically some obscure guidelines which they do not understand in the first place.

If you are part of an agile organization, have you ever taken a step back to create distance between yourself and your work and reflected on how you do things in your organization? Is the Agile approach better than what you had before? If yes, why is it so? What adds *true value*? What has improved and in what way?

These questions should be easy to answer, especially by anyone who is part of an organization that has spent enormous amounts of effort and money in a so-called, agile transformation, and yet, they prove astonishingly difficult. In this blog post, I will try to put in words what *I believe* the true Agile mindset is.

# The problem

Before attempting to provide a solution, one has to really understand the problem. So, let's try to delve into it. Let's study the following, hypothetical case.

A company decides to become Agile and use Scrum. An Agile coach is hired and the so-called Agile transformation begins. The offices are rearranged, new shiny boards are installed and Scrum Master and Product Owner roles are born and filled. Every two weeks a new sprint begins. Its goal is a chunk of the promised-to-the-client release in a few months time. People stand up for no more than 15 minutes a day, discussing their progress and coordinating. The walls are full of sticky notes describing tasks. The software engineers still write code in the exact same way they did before, but now in 2-week iterations. No other department has changed the way it works, apart from the engineering department.

Now, I repeat that this is a hypothetical scenario, but to the extent of my knowledge, a very realistic and typical one. This *"transformation"* is doomed to fail. It is precisely this kind of *"transformations"* that have caused a lot of people to lose faith in the Agile way of working. This approach is fundamentally flawed. It completely misses the essence. It defeats the purpose. Situations like these are commonly described by the term *Agile theater*.

Let's examine what's wrong with this approach. The core idea of the Agile mindset is that

> the people who need the software (stakeholders/users) collaborate closely with the people who make the software and they are able to adjust the course as often as needed

We will discuss how this may be achieved later on, but first, let's understand why the above-mentioned changes do not serve this goal.

 * Releases are planned and promised to the customer with certain deadlines. This does not allow for *adjusting the course*. Despite the pseudo-iterations, the work is treated in a *waterfall* manner. The software engineers break the release work down to 2-week chunks, but that *offers nothing* without the rest of the stakeholders and the customer actively participating in that 2-week loop. *The course cannot be adjusted*.

 * The software engineers have *changed nothing* in the way they write code. Even if the stakeholders and the customer were actively engaged in the loop and even if the course *was* adjusted every two weeks or so, how could the software engineers respond to that? *They couldn't*. If you were to take just one thing away from this post, let it be the following: **Changing the process means nothing without changing the way code is written**

 * Everything *seems* Agile from the outside, but nothing is really changed. Hence the term *Agile theater*. There are neither hooks in the process nor the technical foundation required for constant inspection and adaption. Feedback is not flowing between the software engineers and the stakeholders/users.

# Feedback loops

A truly agile way of working requires constant adaptations. Constant adaptations require a constant flow of feedback. Therefore, lots of feedback loops are needed. The shorter these loops are, the more adaptation they will allow for. The sooner one receives feedback on one's action, the easier it is to amend mistakes.

A feedback loop may sound like a subtle concept, but if you think about it's *powerful* and it's everywhere:

 * Scrum events are feedback loops. During the daily scrum, the team adapts the upcoming day's work based on the feedback on yesterday's work. During the sprint retrospective, the team generates feedback on the previous sprint and makes amendments for the upcoming sprint. During the sprint review, the stakeholders provide feedback on the delivered increment and the product backlog gets adjusted based on it (*sprint review is so misunderstood that perhaps deserves a blog post of its own*).

 * Test-Driven Development (TDD) is a feedback loop. A very short one actually (when done right). The engineers set up a loop between themselves and the code. A change in the code produces immediate feedback. Did the change work? Did it break anything? Does the code written in the last few seconds need modifications? *This actually constitutes the fastest feedback software engineers will ever get on their code.*

 * Pair programming is a feedback loop. This loop is set up between the two engineers working together. The code one writes produces feedback from the other, which changes the code, which changes the feedback and so on and so forth.

 * Code reviews are a feedback loop. Actually, it is the exact same loop with pair programming, except that it involves more people and the feedback flows *significantly slower*.

# Enabling inspection and adaptation

Feedback loops are *enablers*. Remember, we need to adjust our course as often as needed based on feedback. How can we adapt the product to feedback if we don't get any from the stakeholders?

Suppose we do get feedback on a regular basis. How can we utilize it if our technical practices do not support changing easily? The XP technical practices (TDD, pair programming, refactoring etc) enable software engineers to work in a way that expects frequent changes and - as discussed - they constitute feedback loops.

For our feedback loops to be valuable, not only do they need to be in place, but we need to make sure that they are short as well. Getting feedback after a 6-month release, in order to plan the next one, technically is a feedback loop. Not one that can be useful in Agile environments though. Six months is an aeon on a typical market and it is almost impossible to meaningfully predict the needs imposed by the market in such a long period. The release features are doomed to become obsolete to some extent. 

A unit test suite that needs 15 minutes to run is technically a feedback loop, but again, not a useful one. There is no way an engineer can perform TDD using this test suit. The TDD cycle is going to be way too slow to be useful.

To work in an Agile way we need to strive to *keep our feedback loops as short as possible*. We need to shrink them, so long as we keep them meaningful. The shorter the loop the quicker the feedback and therefore the adaptation.

# Scaffolding

Now let's assume that we could do all these things. We could flip a magic switch and, starting from tomorrow, we could create more feedback loops, shorten them, use their feedback to adapt, embrace all XP technical practices etc. 

Why would it make sense to use an Agile framework then? Changes create discomfort. It's natural. Especially when they are radical and they concern the way we work every day. What would Scrum, Kanban, SAFe, LeSS, you-name-it provide that would justify this tremendous effort and energy needed to adopt them? Take a minute to reflect before proceeding.

My answer would be a resounding *"nothing"*. If we already enjoy all the merits that these frameworks bring, why bother adopting them?

However, this magic switch does not exist. That's were the frameworks come into play. They can be used to *initiate* the transition and help us create all these good habits. They can provide the time and place for feedback loops to be created and their feedback to be used. They would put us on the right track and *help us identify what works best for us*. They can be our guide to the exploration of the shift to the Agile mindset. They are great as long as they are used as *scaffolding*.

Getting passed the scaffolding stage *they should be gradually thrown away, giving way to our own, unique Agile process as it emerges*. The process that works best for us.

Failing to throw them away and adjust the process in a way that suits our needs and work defeats the purpose. Frameworks are there to put us on the right track and not be blindly followed to the letter, in a ritualistic way. *Applying them dogmatically only implies a cargo cult mentality*. Doing things without understanding why and expecting certain results to just happen is precisely the definition of *cargo cult*. 

The Agile mindset is centered around autonomous teams, working in a self-organized manner. What are the chances that two autonomous, self-organized teams will need and use the exact same process to the letter? 

> If a process is the same for everyone, it is not Agile

Dogmatically following a framework (e.g. Scrum) to the letter results in everyone doing exactly the same. 

Don't get me wrong. The process that works best for you may be ridiculously close to Scrum (or Kanban etc). I only suggest that these frameworks need not be followed blindly to the letter.

# Never stop learning

Being a Scrum Master myself, I've fallen prey to the frameworks too. During my early days getting passed the Scrum Master training, if the daily stand-up was reaching the 16th minute, I thought that my whole professional world was falling apart. I felt obliged to make the team see that is *should* have been stopped earlier, even if the team wrapped up and finished the stand-up in a total of 16-17 minutes. It still felt wrong. I was myself a victim of the above-mentioned cargo cult mentality.

However, thinking back, I find it quite reasonable. It's a natural step in the learning process. To master something one has to first understand it perfectly and know it inside out. One has to apply it and practise it a lot until one is able to decipher its true meaning and master the skill.

Working with a team will not make you a Scrum Master / Product Owner / Agile Software engineer. A certification will **definitely not** make you one (and I own a certification too). Instead, go out in the industry and work with teams. Listen closely and try to help them. Take time to reflect and identify what works. Above all, never stop learning and be open to changing your mind or standpoint.

# Conclusion

Almost 20 years ago a few people got together and tried to uncover better ways to make software. The message got lost in the way. The intention became misunderstood. The end result is a cargo cult mentality that follows rules blindly, creating more problems than it solves. Job titles and certifications are born, but these don't change the way software is being written.

Agility is based on the idea of constant adaptation based on feedback. Feedback from the stakeholders, the users, the market, the code and our fellow software engineers. The way to get this is to establish feedback loops and make sure that they are short enough to have meaning and be helpful. These will enable constant inspection and adaptation.

Agile frameworks are out there to put people on the right track and not to be followed religiously. They are tools and should be used to help us uncover *our* better ways of making software. As time goes by they should naturally give way to the process that works best for us. A continuous learning mentality will support this gradual transition.
