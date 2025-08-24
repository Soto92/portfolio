---
title: "Software Design: Tactical or Strategic Programming? (Reviewed, Version 2)"
date: "2025-08-24"
featured: true
draft: false
description: "Exploring the balance between tactical and strategic programming in software design: how to handle complexity, dependencies, and long-term sustainability."
tags:
  [
    "software design",
    "programming",
    "tactical",
    "strategic",
    "best practices",
    "agile",
  ]
categories: ["Software Engineering", "Programming"]
authors:
  - admin
# Featured image
# To use, add an image named `featured.jpg/png` to your page's folder.
image:
  filename: "brownfield.jpg"
  focal_point: "center"
---

# Software Design: Tactical or Strategic Programming?

![engineer](engineer.png)

Software Design aims to isolate complexity and simplify code, making it easier to fix, maintain, and reuse in the future.

In development teams, it’s common to plan which technologies to use, which architecture to follow, or which methodology and design patterns to adopt. But surprisingly, little is said about **software design itself**—or about which approach to programming to follow: **tactical or strategic**.

Before diving into these two approaches, let’s take a quick look at what software design really means.

## What is software design?

Software design is about **structuring and organizing code** so that it remains sustainable in the long run. This involves:

- isolating complexity
- modularization
- identifying and addressing critical areas
- anticipating future issues
- fixing technical debt

In other words, software design is not something that happens only at the start of a project. It must be present throughout the system’s lifecycle. It also fits well with agile methodologies: by working in small increments, you can spot problems early, fix them quickly, and prepare the code for future changes.

> “Software is malleable, unlike physical systems. You can change software in the middle of its construction, but you can’t change the number of towers that support a bridge.”  
> — _A Philosophy of Software Design_

## Symptoms of complexity

Good design makes a system **obvious**—easy to understand and simple to modify. When that doesn’t happen, complexity emerges, often visible in symptoms such as:

- **Code repetition**
- **High cognitive load**: the programmer needs to know too much to complete a task
- **Difficulty locating where to change** a given rule or functionality

Complexity usually stems from two main sources: **dependencies** and **obscurity**.

- Poorly managed dependencies cause small changes to ripple across the system.
- Obscurity happens when important information isn’t obvious: poorly named variables, inconsistent naming, unclear data types.

These issues don’t appear overnight. They accumulate gradually until the system becomes hard to maintain.

## Tactical vs. Strategic Programming

This is where programmers come in. How do they apply (or ignore) software design in their daily work?

In practice, we can identify two main styles:

### Tactical programming

This is the approach of those who focus on quick fixes without considering long-term impact. Who hasn’t worked with a “super fast” or “ninja” colleague who delivers features in hours and magically fixes bugs?

![horse](horse.jpeg)

Often, this developer skips tests, writes “do-it-all” methods, ignores proper typing, and only cares about making it work. The result is fragile code, hard to maintain, known as a **brownfield**—an infertile, abandoned area where nothing new grows easily.

![brownfield](brownfield.jpg)

Such systems quickly turn into nightmares: each new feature becomes expensive, and in many cases, rewriting from scratch is cheaper than maintaining.

> “If you develop iteratively and don’t apply agile engineering practices, your codebase will die in two or three years… Ignoring design in an iterative process makes the project unsustainable.”  
> — _James Shore_

### Strategic programming

On the other side, we find the strategic programmer. This profile thinks ahead: creates well-defined modules, reuses code when it makes sense, applies clear naming conventions, isolates complexity, and documents enough so others can easily maintain the system.

![ok](ok.gif)

Their mindset follows the scout principle:

> “Leave the place better than you found it.”  
> — _Baden-Powell_

## The balance needed

So, to conclude, should we follow this "cake recipe" and be super strategic, isolating everything that is function and method for reuse? No! Absolutely not.

![what](what.gif)

But let’s be clear: being strategic doesn’t mean abstracting everything. It doesn’t always make sense to modularize every detail or create reusable layers that will never actually be reused.

The key is balance:

- Is it worth extracting a method that will only be used once?
- Does it make sense to build a generic component without real evidence of reuse?

Being strategic is, above all, about **evaluating the future value of an abstraction**.

## Final tips

- Speed **does not replace** strategy
- Strategic design creates more sustainable projects
- Always plan the future of each User Story, even in small increments
- Clear code + good documentation = easier maintenance
- Gradually invest in design (10% to 20% of development time)
- Avoid being the “Go Horse!” programmer

---

Thanks for reading, and see you next time!

[First version in Portuguese](https://www.ilegra.com/pt/blog/design-de-software-programacao-tatica-ou-estrategica)
