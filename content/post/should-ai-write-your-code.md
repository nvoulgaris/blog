+++
title = "Should AI Write Your Code?"
date = "2025-07-21"
image = "img/posts/should_ai_write_your_code.jpg"
tags = ["AI"]
description = "When to trust it, when to override it and how to stay a responsible engineer"
+++

Why should I spend 40 minutes implementing this when I can explain what I want to Cursor in 3 minutes and have it done immediately? That question crosses the minds of software engineers more and more each day. I know it crosses mine a lot lately. But what do you answer and why?

How much should we use AI tools in software engineering? How do we know when to stop? What are the risks? What should we do with the code that they produce? Blindly check it in?

AI is clearly here to stay and these are questions we need to answer sooner rather than later.

## The AI toolkit for software engineers

Before we answer these questions, let's briefly outline the key tools for AI-assisted software engineering:

- **Cursor**:
  * A fork of VS Code with deep AI integration.
  * Enables inline code edits, chat with your codebase, and powerful refactoring support.

- **GitHub Copilot**:
  * Available in VS Code, JetBrains IDEs, and Neovim.
  * Offers real-time code suggestions, especially strong with common libraries and frameworks.

- **ChatGPT (OpenAI, with GPT-4.5 Turbo or custom GPTs)**:
  * Available via web interface and API; integrates with tools like Raycast and Cursor.
  * Excellent for code reviews, architecture planning, debugging, and explanations.

- **Claude (Anthropic)**:
  * Web-based, with Claude 3 Opus/Sonnet/Haiku models supporting large context windows.
  * Great at understanding and editing large codebases or multi-file PRs.

- **Gemini (Google)**:
  * Available via Gemini web app, Android Studio, and Google Cloud tools.
  * Offers code generation, explanations, and documentation help, especially in Google ecosystems.

- **Perplexity AI**:
  * Not a code generator per se, but a powerful AI search engine.
  * Ideal for technical research, documentation lookup, and comparing code practices.

## Where AI shines

AI tools excel in areas that are predictable, repetitive, and well‑defined. When you know exactly what you want and there's a well-defined way to do this, AI can speed things up considerably. The common characteristics of such tasks are that they are **repetitive, boring, low-risk and don't require any major decisions**. Let's go over some cases:

- **Boilerplate code**: Scaffolding REST endpoints, serializers, data classes, DTOs, and configuration files.

- **Repetitive transformations**: Converting DTOs, migrations, and renaming variables.

- **Code suggestions in familiar frameworks**: Whether it’s React components, Spring services, or Express routes, AI learns common idioms. When you’re working in a well-documented stack, suggestions tend to be accurate.

- **Debugging and quick fixes**: Spotting typos, off‑by‑one errors, missing null checks, or simple logic issues.

- **Light documentation and comments**: Summaries of functions or shorthand explanations of business logic.

- **Implementing another identical feature**: Adding a simple feature (e.g. another CRUD endpoint) to an existing application, when an identical one already exists.

With the right prompt, AI tools can often perform these tasks more efficiently - and faster - than a human engineer, leaving both a solid outcome and more quality time for the tasks that we'd better not leave to them.

## Where it struggles

When the task at hand requires a **solid understanding of context, careful trade-offs, or creative problem solving**, then things are different. In these cases - at least as of July 2025 - the output of AI tools might look reasonable at first glance, but scratching the surface we'll often find wrong assumptions, missing edge cases, or decisions made without justification.

These tasks are **high-risk, ambiguous**, and often **involve decisions that depend on domain knowledge or architectural constraints**. This can be mitigated by providing and gradually building the context for the tool, but it remains a far-from-ideal case to use AI tools to write the code. Let's go over some examples:

- **Core business logic**: Anything that captures product rules, pricing strategies, scheduling, compliance, or other real-world constraints is usually too nuanced for AI to handle correctly.

- **Design decisions**: Choosing between two approaches, introducing a new abstraction, or refactoring involves trade-offs that AI might not understand. It may produce a solution that is not properly justified.

- **Code that hasn’t been written yet**: When you’re building something truly new, with no examples to draw from, AI often fills in the gaps with educated guesses. These guesses can be misleading and are rarely production-ready.

- **Security-critical or performance-sensitive code**: AI has no intuition for attack surfaces, memory constraints, or performance bottlenecks. These are areas where even experienced engineers need to treat carefully.

In short, AI is not a substitute for architectural thinking or deep product knowledge. It’s a great assistant, but a poor decision-maker. The moment a task requires understanding why - not just how - you’re better off taking the lead yourself.

## Trust but verify

No matter how simple the task may be or how competent this particular AI tool is in this type of task, we need to always review the outcome carefully. Every line of code that the AI tools produce should be reviewed twice as carefully as if it was written by a human software engineer. AI can make assumptions or omissions that a human wouldn't make.

It might silently choose the wrong data structure, mishandle a boundary condition, or produce logic that only works in the happy path. And because the code often looks clean and plausible, it's easy to overlook these flaws.

Even for seemingly safe tasks, you should double-check the intent, edge cases, and broader impact. No matter how much you build the context, AI tools don’t understand the domain, the team's conventions, or the long-term consequences like you do.

**The bar for code review should not go down because an AI tool was involved. If anything, it should go up.**

So, use AI to write faster, but make sure you stay responsible for what goes into version control.

## If you can’t explain it, don’t ship it

In my opinion, there is a red line that should **never** be crossed.

> Never ship code that you cannot understand!

It doesn't matter whether the code came from AI, Stack Overflow, or a colleague. It doesn't matter if the tests pass. It doesn't matter if the tool has the best reputation. If you can't explain what it does, why it works, and how it fits into the broader system, it shouldn't be checked in.

AI tools can generate code that works, or at least appears to. But correctness is not the same as clarity. If you can't walk someone through the logic or reason for its behavior under edge conditions, you're taking a blind risk.

This isn't just about debugging or maintenance. It's about ownership. Once the code is merged, it's your responsibility. If it breaks or causes problems later, you can’t blame the tool.

When in doubt, take the time to understand it. If you can't iterate until you reach a version that you fully understand. AI should make us faster, not careless.

## Common pitfalls and how to avoid them

Even with the best intentions, it's easy to fall into habits that undermine the benefits of AI tools. Here are some common mistakes that can find their way into your workflow and how to stay clear of them:

- **Letting AI lead the design**: You should be acting like an architect and AI should be following your lead, not the other way around.

- **Not building enough context**: Poor output often comes from missing domain info, surrounding code, or constraints. Invest time in giving the tool the right context and refine it as the session progresses.

- **Writing lazy prompts**: The quality of the result is directly reflected in the quality of the prompt. Assuming that AI "will understand" is a fundamental mistake. Investing effort in writing a high-quality prompt always pays off. A follow-up post will dive deeper into this.

- **Overusing AI**: If the cost of reviewing the AI’s code is higher than writing it yourself, it’s probably better to just write it. 

- **Skipping tests or reviews**: “AI wrote it” is never a reason to skip your due diligence. If anything, this code deserves more scrutiny, not less.

- **Losing your engineering instincts**: Relying too heavily on AI can dull your ability to spot smells, catch subtle bugs, or reach for the right abstraction. Use AI to support your thinking, not to replace it.

Remember that the tools are getting better, but our responsibility as engineers stays the same.

## Conclusion

AI is here to stay. A number of excellent AI-powered tools are at our disposal and not using them seems suboptimal. However, there's a fine line. A line that we should always have in mind. There are things that AI thrives on, such as writing boilerplate code, scaffolding applications, writing docs and even adding whole simple features when similar ones are already implemented. However, there are also tasks that it wouldn't be wise to trust them completely to an AI tool, such as implementing core business logic and making architectural decisions.

Delegating the right tasks to AI tools is smart, but it’s no silver bullet. Code should be reviewed, tested and - most importantly - fully understood. If it's not, we are in dangerous waters, closer to wishful thinking than to professional software engineering. As we grow more experienced, we should learn to avoid common pitfalls, such as using poor prompts, not providing enough context to the tool and relying blindly on AI tools, without critical thinking. Let's use these tools to make software engineering faster and better, not careless and untrustworthy.

*Have you used Cursor, Copilot, or ChatGPT in your daily development? What worked and what didn’t? Share your experience below.*
