+++
title = "Writing Effective AI Prompts"
date = "2025-10-22"
image = "img/posts/writing_effective_ai_prompts.jpg"
tags = ["AI"]
description = "How LLMs think and how to guide them toward high-quality outputs"
+++

Who hasn’t spent hours going in circles with ChatGPT or Cursor, only to realize that doing the work ourselves would have been quicker and more satisfying? I’ve been there. It’s frustrating. *If only it could understand what I really want.*

But the problem isn’t the AI. It’s how we talk to it. LLMs are powerful tools and, like any tool, knowing how to use them makes the difference between crafting something wonderful and producing something unnatural. Thinking that the LLM "will understand" is a road that more often than not leads into long rabbit holes, hallucinations, and frustration. We need to understand how they work. Learning to prompt the LLM right is a skill that turns AI from a distraction into an accelerator.

So, let's first understand how they work and then how we can trigger them to get what we want every time.

## How LLMs work
Large Language Models (LLMs) belong to the branch of generative AI. While "traditional" AI analyzes data and supports decision-making, generative AI creates new content, such as text, images, or code. LLMs in particular focus on language.

They are able to predict the next token (word or punctuation), working in a **probabilistic way**. Given an input, they use a neural network to assign a probability to each token, and the one with the highest probability becomes the next token. It's important to understand that they have **no capacity for reasoning** and they do not work in a deterministic way.

Think of an LLM as an extremely advanced autocomplete engine. It doesn’t *understand* your question. It predicts what a good answer might look like *based on patterns* in its training data. That’s why how you ask matters more than what you ask. Your words shape the probabilities. Triggering the LLM in the correct way is key to producing the desired output.

Now that we know why LLMs behave this way, let’s see how we can guide them effectively.

## Prompting Techniques: The Basics
Before delving into specific prompting frameworks and examples, let's briefly go over the basic prompting techniques as well as the tasks for which they are a good fit.

### Zero-shot prompting
Zero-shot prompting is applied when asking the LLM to perform a task **without providing any prior examples**. So, this relies solely on the model's pre-existing knowledge to understand and complete the task. This technique can be a good fit for simple, straightforward tasks.

### Few-shot prompting
In this case, **a few examples of the desired input-output are provided** within the prompt. These examples act as specifications, guiding the LLM and helping it understand both the task and the format of the input and output more quickly and more accurately. This is a useful technique when the task requires a specific output format or when it is too complex for a zero-shot prompt.

### Chain-of-thought prompting
Chain-of-thought prompts encourage the LLM to **show its work by thinking step-by-step** before providing an answer. They explicitly ask it to break down its reasoning process. This leads to more accurate and transparent outputs. This is ideal for complex problems that require multiple steps of reasoning.

These basic techniques are great building blocks, but if you want consistent, high-quality outputs, structured prompting frameworks take it a step further.

## Prompting frameworks
Now, let's dive into specific prompting frameworks and the ideal use cases for each one.

### RTF (Role - Task - Format)
I use RTF when I just want the model to “get in character” and give me something clean. You tell it who to be, what to do, and what the output should look like. It’s simple, but surprisingly powerful when you want predictable output.

**Best suited to**: Code writing, debugging, or documentation where you want clarity and structured output.

Example:
```
Role: Senior Java developer  
Task: Write a unit test for a service that sends email notifications.
Format: Provide only the Java code inside a code block.
```

### CODE (Context – Objective – Details – Expectations)
This is what I use when I need to be crystal clear. It’s like writing a mini design doc before asking the LLM for help. You give it the background, the goal, the details, and what you expect at the end.

Perfect for when you need structured answers that actually fit your setup, not some generic solution from a random Stack Overflow thread.

**Best suited to**: Code writing for context-aware results that align tightly with the existing code.

Example:
```
Context: We’re building a REST API for a task management app using Spring Boot and Kotlin.  
Objective: Generate a controller method for creating new tasks.  
Details: The Task entity has title, description, and due date.  
Expectations: Provide only the function and annotate it correctly for a POST endpoint.
```

### CO-STAR (Context - Objective - Style - Tone - Audience - Response format)
This is basically your tone dial. If you’re writing docs or commit messages and want them to sound human, not robotic, this is your friend. You tell the model what the situation is, what you’re trying to achieve, and who’s reading it. It will match your voice surprisingly well.

**Best suited to**: Producing technical documentation, API specs, or explanations tailored to a specific audience.

Example:
```
Context: We’re adding a new message queue for background jobs.  
Objective: Explain the architecture to a new backend hire.  
Style: Conversational but technical.  
Tone: Encouraging.  
Audience: Junior backend developer.  
Response format: Numbered bullet points.
```

### RISEN (Role - Instructions - Steps - End goal - Narrowing)
RISEN is what I reach for when I need the model to walk through something methodically, like setting up a CI pipeline or migrating a project. You define the role, the overall task, break it into steps, and tell it where to focus. It keeps the conversation grounded instead of spiraling into theory.

**Best suited to**: Complex, multi-step engineering problems, such as setting up CI/CD or refactoring large codebases.

Example:
```
Role: DevOps engineer.  
Instructions: Explain how to set up GitHub Actions to build and test a Kotlin multi-module project.  
Steps: Provide them sequentially.  
End goal: Fully automated CI pipeline.  
Narrowing: Assume tests use JUnit 5 and Gradle.
```

### RACE (Role - Action - Context - Expectation)
RACE is my go-to for code reviews. You set the model’s role (say, “experienced reviewer”), tell it what kind of issues to look for, give it the context, and explain what format you want the feedback in. The output feels like a real teammate’s review, not a lecture.

**Best suited to**: Fast, direct code fixes or reviews without overloading with background details.

Example:
```
Role: Kotlin code reviewer.  
Action: Identify potential NPE risks in this function.  
Context: Function runs in a Spring Boot service with nullable database fields.  
Expectation: List only the risky lines and a short fix.
```

### Chain of Thought (CoT)
CoT is your “think out loud” mode. You literally tell the model: “Walk me through this step by step.” It’s brilliant for debugging or tricky logic, like having a second brain narrate its reasoning.

**Best suited to**: Problem-solving that requires reasoning, such as algorithm design or debugging some tricky logic.

Example:
```
Think step-by-step:  
Given this recursive Kotlin function for DFS traversal, explain why it fails on cyclic graphs and how to fix it.
```

### Tree of Thoughts (ToT)
ToT takes CoT up a notch. Instead of one straight line of thought, it branches out, exploring a few possible paths before settling on the best one. I like it for architecture decisions or design trade-offs where you want the AI to think in options, not absolutes.

**Best suited to**: Exploring multiple design/implementation approaches before committing (e.g. for API design trade-offs or database schema planning). This is ideal for complex decision-making.

Example:
```
Explore different approaches:  
We need to design a REST API for a booking system. List three possible resource structures, evaluate pros/cons for each, then recommend one.
```

### CARE (Context - Action - Result - Example)
CARE works great when you want the model to see what good looks like. You tell it what’s going on, what needs to happen, what the outcome should be, and then show it an example.

It’s like pair programming with a demo first.

**Best suited to**: Teaching best practices or explaining patterns with examples.

Example:
```
Context: We’re migrating from Java to Kotlin in a Spring Boot app.  
Action: Show how to replace anonymous classes with lambdas.  
Result: Cleaner, idiomatic Kotlin.  
Example: Provide a before/after code snippet.
```

Once you start using these regularly, you’ll notice that they’re not rigid formulas. They’re just ways to steer the model’s attention. Pick one, tweak it, and make it yours.

## Reference table
To make it easier to pick the right one at a glance, here’s a summary comparing how each framework performs in typical software engineering tasks. It can be [bookmarked](#reference-table) and used for quick referencing.


| Framework                                                                     | Code Generation | Debugging | Architectural Design | Documentation | Strengths                                                                                  |
| ----------------------------------------------------------------------------- | --------------- | --------- | -------------------- | ------------- | ------------------------------------------------------------------------------------------ |
| **RTF** (Role • Task • Format)                                                | ✅✅✅          | ✅✅      | ✅                   | ✅✅          | Straightforward and reliable for focused coding tasks and clean outputs.                   |
| **CODE** (Context • Objective • Details • Expectations)                       | ✅✅✅          | ✅✅      | ✅✅                 | ✅✅          | Excellent for precise, context-aware results that align tightly with your setup.           |
| **CO-STAR** (Context • Objective • Style • Tone • Audience • Response format) | ✅✅            | ✅        | ✅✅                 | ✅✅✅        | Best for documentation or explanations tailored to a specific tone or audience.            |
| **RISEN** (Role • Instructions • Steps • End goal • Narrowing)                | ✅✅            | ✅✅      | ✅✅✅               | ✅            | Ideal for multi-step workflows like CI/CD setups, migrations, or structured tutorials.     |
| **RACE** (Role • Action • Context • Expectation)                              | ✅✅            | ✅✅✅    | ✅                   | ✅            | Great for quick, focused reviews or targeted code fixes.                                   |
| **Chain of Thought (CoT)**                                                    | ✅              | ✅✅✅    | ✅✅                 | ✅            | Encourages reasoning and transparency in problem-solving and debugging.                    |
| **Tree of Thoughts (ToT)**                                                    | ✅              | ✅✅      | ✅✅✅               | ✅            | Explores and compares multiple design or implementation paths before deciding.             |
| **CARE** (Context • Action • Result • Example)                                | ✅✅            | ✅        | ✅                   | ✅✅✅        | Excellent for illustrating best practices and teaching with before/after examples.         |

✅✅✅ = Excellent fit  
✅✅ = Good fit  
✅ = Somewhat suitable

## Conclusion

LLMs have already become an integral part of our day-to-day workflow. Learning how to best use them is quickly evolving into an invaluable skill for any software engineer. They do not think. They produce content based on pattern-matching and probabilities. So, the better we ask the question, the better the output will be.

Depending on the task, we can provide examples or we can ask the LLM to provide its reasoning process. Using the right framework can be a key difference between a prompt that got the job done versus one that threw us into a rabbit hole.

Next time you catch yourself fighting the AI, pause and reframe your prompt. You’ll be surprised how often that’s all it takes.
