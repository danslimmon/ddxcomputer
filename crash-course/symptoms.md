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

## Example

The DDx kickoff has arrived, and the *Vasa* dev, the SRE, and the support rep all ~walk into a bar~
join the video call. You welcome everybody and give a brief synopsis of the differential diagnosis
process that you're all about to undertake.

Once everyone's on the same page about the general process, you begin the first step: writing down
symptoms.

```
diagram of example network
```

You write down a couple of symptoms off the top of your head, to get some momentum going:

* Sporadic customer-facing errors from *Vasa*: `Error retrieving payload from Argos: HTTP request
  failed.`
* No corresponding access log messages from *Argos*

Now you stop writing and wait for the rest of the troubleshooting squad to shout out more systems.
After a pregnant pause, the support rep pipes up:

* These errors only seem to occur during periods of high traffic volume

Next to speak is the *Vasa* engineer. "Well," he opines, "one symptom is that *Argos* is dropping
requests, right?"

You furrow your brow. "I don't know that I'd call that a symptom. We haven't directly observed any
requests getting dropped, and symptoms are things we directly observe. What you're giving us is more
of a hypothesis about _why_ we're observing these symptoms. So why don't you hold that thought until
we get to the next phase?"

And so it goes. After a few rounds of call and response, the symptom list looks like this:

1. Sporadic customer-facing errors from *Vasa*: `Error retrieving payload from Argos: HTTP request
   failed.`
2. No corresponding access log messages from *Argos*
3. These errors only seem to occur during periods of high traffic volume
4. Multiple different customers have experienced this issue while trying to perform multiple
   different kinds of operations
5. The frequency of this failure mode has been increasing gradually for at least 3 months

At this point, you judge that you've written down enough symptoms to describe the problem under
investigation. An interested party would be able, by reading this symptom list, to grasp the scope
and character of the issue. After making sure nobody has any last-minute additions to the list, you
proceed to the next phase of DDx: generating hypotheses.

**Next:** [Hypotheses](hypotheses)
