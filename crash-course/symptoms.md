---
layout: "page"
title: "Symptoms – DDx crash course"
permalink: "/crash-course/symptoms"
---

**Back to:** [Home](intro)

**Next:** [Hypotheses](hypotheses)

Once a problem has been identified and a team has been assembled to do DDx, the team gets together
and runs through their first DDx session. The first step: identify **symptoms**.

A symptom, as we define it, is:

> Any piece of information we've obtained about the problem by directly observing the system.

During the Symptoms phase of DDx, the team tries to write down as many of the symptoms as they can
think of. Symptoms may be based on things you've seen, like _This error is thrown on the homepage
on about 1 in 10 page loads_. They may also be things you've learned from the _absence_ of
confirming evidence, such as _This error is never thrown if the request is coming from the VPN_.

This is one of the places where having a team with lots of diverse perspectives is most important.
A network engineer may see very different symptoms than a support rep, and you'll benefit from
writing down both sorts of symptoms.

## Minimize inference

The Symptoms phase is about writing down what we know. To that end, it's important to state symptoms
as objectively as possible. Avoid the temptation to make logical inferences from observations.
That's what we'll do in the next step. But in order to keep our minds open about what could be
_causing_ the symptoms we observe, we first need to faithfully record what exactly we're observing.

For example, if you notice that whenever a certain type of request is sent, the server fails to log
that request in its access log, it might be tempting to write down:

> Server does not receive the request.

But that would be an inference. During the Symptoms phase of DDx, it would be better to write down
something more directly based on observation, such as:

> The request is sent, but the server does not log the request.

This formulation leaves room for other explanations: it may be true that the server doesn't receive
the response, but it may also be that the server receives the request but crashes before it gets a
chance to log it. Or there may be some other explanation. An objective statement of the symptom
leaves room for us to think more creatively about the problem at hand when we proceed to the second
phase: Hypotheses.

**Next:** [Hypotheses](hypotheses)
