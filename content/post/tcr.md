---
title: "Test && commit || revert"
date: "2021-03-07"
tags: [tcr]
image: img/posts/tcr.jpg
---

The test should pass now. Oh, it still fails. Why is that? I think I've missed this edge case. I'll fix it by adding this line, here. Great, it passed, but another one fails now. That's weird. I guess that this line broke the other case. Never mind, I'll add this line too and this should fix both of them. Oh, now I've broken a bunch of them. Perhaps I need to re-write this class.

Have you ever been in a situation like this? Do you relate to the train of thoughts? How long did it take you to get all the tests to pass? How did you feel when they finally passed? Creative, energized and ready to continue or relieved, exhausted and ready to take a break or call it a day? What if you had *reverted* the change as soon as it made a test fail and approached the problem from a different angle?

This is one of the key ideas behind *test && commit || revert* (TCR), a programming workflow born during a Kent Beck workshop (and also attributed to Oddmund Strømme, Lars Barlindhaug, and Ole Johannessen). So, in this blog post, I will try to provide an overview of TCR.

*Before we delve into it, let me add a small disclaimer. I have only scratched the surface of TCR. I have only used it in playground projects, with the sole purpose of understanding it. I have not used it in production code and I am definitely not advocating for it in this post. The intention of the post is to let you know that TCR is a thing and merely present some of its trade-offs that I have discovered.*

# The main idea

During any typical programming workflow, we run the tests a lot. We definitely do so before committing the code. So, the idea behind TCR is that we should commit *every* time the tests pass. But there's a catch. If we do commit every time the tests pass, we should also revert every time the tests fail. It's simple but truly profound.

Applying these two constraints locks us in a cycle. Exactly like TDD does, just with a different cycle. Since a failing test automatically reverts the code, there is no red state. We always keep the tests passing and we always find ourselves in the green state, the only state there is.

{{< figure src="/img/posts/tcr_cycle.jpeg" caption="source: https://medium.com/@kentbeck_7670/test-commit-revert-870bbd756864" alt="source: https://medium.com/@kentbeck_7670/test-commit-revert-870bbd756864" >}}

# Why should I try it

Now, I understand that TCR may sound extreme (to say the least). I can already hear the objections. *"But I will be losing code". "But I love the red state". "But it sounds so irritating". "But why would I want to do that?"*. These were also *my* first thoughts. So, let's try to understand what do we stand to gain from giving TCR a chance.

## Baby steps

If there was a single lesson to be learned from TCR it would be the following: 

> The only way to go fast, it to go well

This is a quote from Uncle Bob, which has shaped my way of thinking around writing code like few others.

The core idea behind TCR is moving in small steps. Moving in baby steps. Tiny steps. Small enough to keep the tests passing. Small enough not to risk losing a bunch of code if a test fails. The mindset is *"what is the next, small, secure step that I can take towards the desired result?"*.

## Continuous delivery

## Better refactoring

Refactoring a piece of code takes discipline. It requires a series of small, confident steps. It requires keeping the tests green at all times. The truth is that, even with the aid of the IDE's automated refactoring options, this is challenging.

I find that TCR can be immensely helpful during the refactoring process. Any modification that breaks the tests gets automatically reverted. Therefore, all refactoring moves keep the tests green.

But there's more in it. Refactoring moves that break the tests get reverted. They do not *"survive"* into commits. Only the ones that keep the tests passing *"survive"*. They get committed and eventually pushed and merged. This rings a bell, doesn't it? This sounds a lot like a *natural selection process for refactoring moves*. Just the ones that display useful qualities (keep the tests passing) make it into commits. The accumulation of the effects of this, continuous feedback makes us more skilled in the long run. Let's not get carried away with the metaphor, but applying TCR when refactoring can really improve our refactoring skills.

## A tool for understanding legacy code

## Gamification

Practice TCR for 10 minutes and it becomes obvious that it gamifies writing code like nothing else I know of. Causing a test to fail feels like making a mistake in a video game and having to start over again. Of course, this coin has two sides (more on that later on), but the bright side of gamification is that it's fun. And when we have fun while writing code, we tend to be more creative and we tend to come up with better solutions.

# Downsides

## Losing stacktraces

I feel that the downside that will be so obvious that you can't ignore it when using TCR is losing the stacktrace when a test fails. It's natural. When a test fails, we want to understand why it failed. However, since the tests get reverted automatically, the stacktrace disappears.

Perhaps there are ways around the issue, by carefully configuring the `test` command you use, but it was the very first thing that annoyed me when a test failed when I wasn't expecting it.

## Losing failed test output

In the same context, I found it very problematic that I kept on losing the test output in general when tests failed. I first noticed it when I used Spock's `@Unroll` feature and a single case failed.

This is part of the process. TCR urges you to approach the problem from a different angle. Or maybe opt for a smaller step, rather than debugging a failed test.

## Commit messages

It should be obvious that practising TCR can easily create tens of tiny commits. Actually, it should do exactly that when done right. So, the questions that naturally follows is *"what do I do with all those commits?"* and *"what about the commit messages?"*.

These can easily be addressed in a number of ways. For instance, my preferred method is to add a default commit message (e.g. "WIP") and, when I reached the point that I would originally commit if I was not using TCR, squash all these, tiny WIP commits to a single one and reword it. Perhaps, applying the `git diff` list as the commit message would work for some other people.

Nevertheless, this constitutes a problem that should be solved and one way or another, it adds an overhead to the work.

## Irritation

The alter ego of the above-mentioned gamification aspect is the irritation that TCR can cause you. The rational first reaction to witnessing the code you've been writing over the past few minutes magically disappearing in front of your eyes is frustration. Sometimes even anger. While gamification can make one more creative, irritation can lead to bad-tempered decisions and hasty solutions.

Unfortunately, this can lead to a vicious cycle. The more the code gets reverted, the worse your mood gets, which leads to more mistakes, which leads to the code getting reverted even more. Quite ironically, this is a *good* feature of TCR. If you find yourself having your code reverted say 10 times in a row, perhaps that's the best sign that you need a break. One has to have the presence of mind in order to benefit from this, *good feature* of TCR though.

In any case, I feel that this is perhaps the most interesting trade-off that TCR has to offer. The balance between having fun and feeling angry and disappointed is crucial. In other words, for TCR to be effective, sticking to the essence is key. And the essence is aiming for *baby steps*.

# Open questions

A programming workflow it's open to customization and experimentation by its nature. TCR, being fairly new (created at 2018), leaves plenty of room for both. Let's examine some of the aspects that remain open.

## Reverting tests

Writing a test only to have it reverted because it failed can be discouraging. Especially for people with a strong TDD background, who have worked hard to install the habit of writing a failing unit test first, this can be particularly disturbing. Maybe this is the reason why it was suggested that the tests should not get reverted as part of the TCR process. In other words, failing tests should revert the production code, but not the tests.

I strongly believe that different approaches may work better for different people. TCR is a tool. It's merely means to an end and not an end in itself. So, I have deliberately chosen to include this topic in the open questions. I believe that either approach will work. So, some people will choose to revert the tests along with the production code and some people will not do so.

## What happens with pushing

We have already discussed the issue with the numerous, tiny commits, but when does the code gets pushed during this workflow? Again, this is a matter of choice. Manually pushing after a bunch of small commits will work fine. Exactly like automatically pushing along with every tiny commit. The issue with the commit messages has to be resolved in either case. So, anything that suits your needs is fine I guess.

# Setting up the environment for TCR

Practising TCR requires a little bit of setup. There should be an automated way to observe the source files that change, run the tests and, depending on the outcome of the tests, either commit or revert the code. There are various ways in which this can be achieved. Personally, I used the following bash scripts:

* a `watch.sh` script that observes the source code and triggers the TCR script whenever a file is modified.

```bash
#!/bin/bash

while true; do
  inotifywait -r -e modify src
  ./tcr.sh
done
```

* the `tcr.sh` script, that hold the base logic of TCR:

```bash
#!/bin/bash

source "scripts/test.sh"
source "scripts/commit.sh"
source "scripts/revert.sh"

test && commit || revert
```

 * the `test.sh` script, which executes the Spock tests

```bash
#!/bin/bash

function test() {
  echo "Testing changes..."
  ./gradlew test
}
```

 * the `commit.sh` script

```bash
#!/bin/bash

function commit() {
  echo "Committing and pushing changes"
  git add . && git commit -m "WIP" && git push
}
```

 * and the `revert.sh` script

```bash
#!/bin/bash

function revert() {
  echo "Reverting changes"
  git checkout .
}
```

I have created a [playground github repository](https://github.com/nvoulgaris/tcrPlayground). It is set up for Kotlin and Spock and serves me for experimenting with TCR, but feel free to either grab the bash scripts or clone it and use it to play with TCR.

# Conclusion

TCR provides an exciting, fresh point of view regarding writing code. It focuses on small, certain steps, which create steady progress. It gamifies programming and, among other things, it can be applied to refactoring and understanding of legacy code.

There are disadvantages to be considered, such as losing the stacktraces and output of failed tests. Dealing with countless tiny commits. Dealing with frustration. There are also a lot of open questions, like whether or not tests should get reverted along with the production code or when should one push the code. 
