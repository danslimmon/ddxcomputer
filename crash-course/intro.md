---
layout: "page"
title: "DDx crash course: Overview"
permalink: "/crash-course/intro"
---

This crash course is designed to give you a solid understanding of the differential diagnosis
framework as we use it in software troubleshooting. You'll learn some fundamental vocabulary, which
we'll use to explore the 3 phases of DDx. By the end, you should have all the knowledge you need to
[start applying DDx in your organization](/getting-started).

## Why DDx works

The differential diagnosis framework originated in medicine. Doctors learn it in medical school, and
the vocabulary of differential diagnosis is prevalent throughout the medical establishment. If
you've ever watched the TV show _House M.D._, you've seen it in action (albeit in caricature).

So DDx is a medical framework. but the parallels between medicine and software are such that we can
benefit enormously by applying the same troubleshooting principles to software and infrastructure
problems. I've been doing just that for over a decade, and this website will show you how to take
adopt DDx on your own team.

**Software systems are complex, like bodies.** Much like a doctor investigating a cluster of
symptoms, when we're troubleshooting software failures we have limited visibility into the system,
a rapidly changing understanding of the problem at hand, and no single person with a full
understanding of all the subsystems involved. Differential diagnosis allows us to navigate the
problem solving effort in these sorts of situations, maintaining common ground with each other as we
move toward a deeper understanding and, ultimately, a solution.

## The 3 phases of differential diagnosis

A DDx troubleshooting effort follows a 3-phase cycle:

* **Symptoms.** Write down everything you know about the problem.
* **Hypotheses.** Think of lots of different explanations for the observed symptoms.
* **Actions.** Decide what to do next to refine your understanding of the problem at hand.

It may not always be clear what phase of the cycle the troubleshooting team is in. In the real
world, different team members will work through the problem in different ways, and hewing too
closely to this formal structure can interrupt their thought processes. But it's a good idea to
establish a **cadence**: a regular interval after which everybody on the team meets to go through
the phases together. This is an opportunity to make sure everyone's on the same page about what the
problem is, and what it isn't.

## Building a troubleshooting team

A word is also warranted here about who should be part of the troubleshooting team. As a rule of
thumb, it's wise to account for as many perspectives as possible. The reasons for this will become
clearer as we dive into each of the phases in more depth. But, as an example, if you're
troubleshooting a problem where certain web requests are returning 500 errors to the client, don't
just pull in web developers. Try to get an SRE, a network engineer, a DBA, and a support rep. Not
all of these people will always have something to do, but they can all stay up to speed on the
troubleshooting effort so they can provide input and jump into the fray when they're needed.

Picking the right set of people is more of an art than a science. But after using differential
diagnosis a few times, you'll start to find the sweet spot between maximizing perspectives and
minimizing the cost of synchronizing people.

More is said on the subject of team composition in the [Getting Started guide](/getting-started).

**Next:** [Symptoms](symptoms)
