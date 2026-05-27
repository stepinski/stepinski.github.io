---
title: "Why I'm Betting My Next Five Years on Go"
description: "On choosing a language for clarity, production durability, and the long arc of a career."
date: 2025-01-20
icon: "⬡"
---

There's a kind of professional decision that looks small from the outside but reshapes everything downstream. For me, the decision to commit to Go as my primary language over the next five years is one of those.

I've been writing software for 15 years. I started in C++ doing IEC 61850 protocol implementations and native desktop GIS tooling. Moved through Scala for ML infrastructure. Built time-series pipelines in Python. And somewhere in the middle of all of that, I noticed that the languages I enjoyed most were the ones that got out of my way.

## What I Mean by "Getting Out of Your Way"

Go doesn't have generics in the sense that will make a Haskell programmer happy. It has a garbage collector that occasionally does things you didn't expect. It lacks the expressive power that Scala has in its type system.

And yet: every Go program I've read from a stranger on GitHub, I could understand within five minutes. That property — *legibility across authors* — is underrated to the point of being invisible until you've worked in a large enough codebase.

The canonical Go approach to error handling is verbose. It is also explicit in exactly the way that matters when you're debugging a production incident at 2am.

## Lark as a Learning Vehicle

[Lark](https://github.com/carldata) is a physics-informed sewer overflow prediction library. It's been in production for Peel Region since 2024. It's also, deliberately, my primary Go learning project.

I could have written it in Python. Python is faster to prototype and has a vastly larger ML ecosystem. But I wanted the resulting artifact to be:

- deployable as a single binary
- embeddable in a larger infrastructure platform without a runtime dependency
- readable by a new engineer without Go experience in under a day

A Go library satisfies all three. A Python package satisfies none of them with the same elegance.

## On Local-First and the CLI Renaissance

Part of why Go appeals to me is adjacent to a broader philosophy I've been developing about software: *local-first, dependency-minimal, and durable*.

I've been building personal tools — note managers, CLI productivity tools, a sewer overflow predictor — with a consistent stack: Go, Cobra, Bubble Tea, DuckDB. No servers. No accounts. No SaaS dependencies that will raise prices or shut down. Just a binary that does one thing reliably.

There's something almost monastic about it. The constraint produces clarity.

## The Five-Year Frame

By 2030, I want to be the kind of engineer who can look at a Go codebase and see it the way a senior Rubyist sees Rails or a long-time C programmer sees the Linux kernel — not just as a language, but as a *way of thinking* that's been internalized.

That requires a level of depth you can only get by choosing something and staying with it through boredom, frustration, and the temptation to chase the new thing.

The new thing is always interesting. Depth is rarer.
