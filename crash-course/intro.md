---
layout: "page"
title: "Overview – DDx crash course"
permalink: "/crash-course/intro"
---

**Back to:** [Home](/)

**Next:** [Symptoms](symptoms)

This crash course is designed to give you a solid understanding of the differential diagnosis
("DDx") framework as we use it in software troubleshooting. You'll learn some fundamental
vocabulary, which we'll use to explore the 3 phases of DDx. By the end, you should have all the
knowledge you need to [start applying DDx in your organization](/getting-started).

## Why DDx works

The differential diagnosis framework originated in medicine. Doctors learn it in medical school, and
the vocabulary of differential diagnosis is prevalent throughout the medical establishment. If
you've ever watched the TV show _House M.D._, you've seen differential diagnosis in action (albeit
in caricature).

So DDx is a medical framework. But the parallels between medicine and software are such that we can
benefit enormously from applying the same troubleshooting principles to software and infrastructure
problems. I've been doing just that for over a decade, and this website will show you how to adopt
DDx on your own team.

**Software systems are complex, like bodies.** Much like a doctor investigating a cluster of
symptoms, when we're troubleshooting software failures we have limited visibility into the system
and a rapidly changing understanding of the problem at hand. Furthermore, there's often no single
person with a deep understanding of all the subsystems involved. Differential diagnosis allows us to
navigate the problem solving effort in these sorts of situations, maintaining common ground with
each other as we move toward a deeper understanding and, ultimately, a solution.

## The 3 phases of differential diagnosis

A DDx troubleshooting effort follows a 3-phase cycle:

* **Symptoms.** Write down everything you know about the problem.
* **Hypotheses.** Think of lots of different explanations for the observed symptoms.
* **Actions.** Decide what to do next to refine your understanding of the problem at hand.

It may not always be clear what phase of the cycle the troubleshooting team is in. In the real
world, different team members will work through the problem in different ways, and hewing too
closely to this formal structure can interrupt their thought processes. But it's a good idea to
establish a **cadence**: a regular interval after which everybody on the team meets to go through
the phases together. This is an opportunity to make sure everyone's on the same page about the state
of the problem solving effort.

## Building a troubleshooting team

Who should be part of team troubleshooting a problem? As a rule of thumb, it's wise to account for
as many perspectives as possible. The reasons for this will become clearer as we dive into each of
the phases in more depth. But, as an example: if you're troubleshooting a problem where certain web
requests are returning errors to the client, don't just pull in web developers. Try to get an SRE, a
network engineer, a DBA, and a support rep too. Not all of these people will always have something
to do, but they can all stay up to speed on the troubleshooting effort, giving input and jumping
into the fray when they're needed.

Picking the right set of people to engage in differential diagnosis is more of an art than a
science. But after using the framework a few times, you'll start to find the sweet spot between
maximizing perspectives and minimizing the cost of keeping people in sync.

More is said on the subject of team composition in the [Getting Started guide](/getting-started).

## Example

Imagine, for one brief, magical moment, that you're a Ruby on Rails developer. Your team owns a
microservice – let's call it *Argos* – whose job is to serve up data to the main customer-facing web
app – which we'll call *Vasa*.

```
diagram
```

Over the last few weeks, people have started to notice an uptick in the number of error responses
coming from an *Vasa* that seem to be indicate a problem retrieving data from *Argos*. You, as the
engineer most familiar with the inner workings of this particular code path in *Argos*, are asked to
investigate and fix this new problem.

However, after a few days of digging, you get more or less nowhere. You can't find any evidence that
*Argos* even received the ill-fated requests from *Vasa*, much less crashed while handling them! But
the error thrown by *Vasa* pretty unambiguously implicates *Argos*:

```
Error retrieving payload from Argos: HTTP request failed
```

What can you do? You're not familiar with *Vasa*'s codebase or even the language it's written in.
The developers of *Vasa*, conversely, don't know anything about *Argos* except that it's supposed to
return payloads of a given form in response to requests. And when you asked the SREs to help you
look for a network issue, they told you it would be like finding a needle in a hay stack.

This is shaping up to be a real [yak shave](https://seths.blog/2005/03/dont_shave_that/). But rather
than continue to spin your wheels for who-knows-how-long, you decide to try out differential
diagnosis. You get hold of a *Vasa* dev, an SRE, and the support rep who's been assigned the ticket
for this issue, and you schedule a DDx kickoff meeting.

**Next:** [Symptoms](symptoms)
