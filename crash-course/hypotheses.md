---
layout: "page"
title: "Hypotheses – DDx crash course"
permalink: "/crash-course/hypotheses"
---

**Back to:** [Symptoms](symptoms)

**Next:** [Actions](actions)

The Hypotheses phase of differential diagnosis is where the real magic happens. Given the symptoms
we recorded in the previous phase, we now try to come up with as many hypotheses as we can. In the
medical community, these hypotheses are referred to as "differentials" – hence the name
"differential diagnosis."

A hypothesis is defined as:

> A plausible, testable explanation for a symptom or group of symptoms.

This is where it really pays off to have a team with a diverse set of perspectives. The more
hypotheses we can generate, the more progress we'll be able to make in the next phase: Actions.

Even if a hypothesis seems unlikely or conflicts with some of the symptoms we've identified, it's a
good idea to write it down. Once we've written down all the hypotheses we can think of, only then
should we go through and figure out which ones we want to reject. As we do so, we can also record
the reasoning that led us to reject them.  Differential diagnosis is all about making our thought
processes explicit so that everybody stays on the same page.

## Testability

Per our definition, the hypotheses that we write down should be **testable**. In practice, this
means that we can in principle find a single piece of evidence that would _disprove_ the hypothesis
(why disprove and not prove? More on that below.)

This testability criterion implies that our hypotheses should be stated as precisely as possible.
Only a precise hypothesis can be disproved (or rendered extremely unlikely) by a single piece of
evidence. For example, it might be tempting to write down a hypothesis like this:

> Packets are getting dropped between the web server and the database.

But in most production architectures, there are several different things this could mean. Maybe we
can show that packets aren't getting dropped on one particular hop, but that piece of evidence won't
necessarily allow us to decide whether this hypothesis is a whole is false. It's probably better to
record multiple more precise hypotheses, such as:

> 1. The web server fails to connect to the database server because its outgoing packet(s) get
>    dropped.
> 2. The web server fails to communicate with the database server once connected because its
>    outgoing packet(s) get dropped.
> 3. The database server fails to send a response back to the web server because its outgoing
>    packet(s) get dropped.

Each of these hypotheses can be proven false with a single packet capture.

## Falsification over confirmation

In DDx, it's usually better to **falsify** hypotheses rather than try to confirm them.

This is one of the trickier things to get used to when you adopt the framework, since most people
think about troubleshooting in terms of trial and error: think of an explanation for the problem,
then go prove yourself right. Differential diagnosis is great for tackling problems that resist this
kind of guess-and-check approach, and that's because it asks us to rule things _out_ instead of
proving them. This is called "falsifying" hypotheses.

One of the most important ways in which the shift from confirmation to falsification helps us reason
about problems is by averting **tunnel vision**. It's easy to get carried away by a hunch that one
particular hypothesis is true, ignoring or neglecting to look for evidence that would point in any
other direction.

Remember: it's always possible that the correct explanation for the problem under examination
has not yet been thought of. By focusing on falsifying hypotheses rather than confirming them, we
can hone in on a cogent and consistent explanation for the problem without getting lured into tunnel
vision.

## Example

```
diagram of example network
```

"Alright," you proceed, "what are some things that could explain these symptoms?" The assembled
troubleshooters ponder the symptoms in the shared document:

1. Sporadic customer-facing errors from *Vasa*: `Error retrieving payload from Argos: HTTP request
   failed.`
2. No corresponding access log messages from *Argos*
3. These errors only seem to occur during periods of high traffic volume
4. Multiple different customers have experienced this issue while trying to perform multiple
   different kinds of operations
5. The frequency of this failure mode has been increasing gradually for at least 3 months

The *Vasa* dev pipes up, reiterating the idea that he initially brought up as a potential symptom:
"*Argos* is dropping requests."

"Okay, I'll put that down. Just to make sure we're not ambiguous: you're saying that requests from
*Vasa* are reaching *Argos* at the TCP level, but *Argos*'s business logic for some reason never
starts handling the request?" The *Vasa* dev nods. You write it down:

* The web server in front of *Argos* fails to pass certain requests to the service.

You could break this down into further hypotheses if you wanted. There could be any number of
reasons _why_ the web server might be dropping these requests, and each of those reasons could be
its own line in the hypothesis section of the DDx doc. But at this point, when you're still trying
to sketch the outlines of the problem, you decide that this hypothesis is just fine. But you do add
another, "sister" hypothesis to describe a slightly different scenario:

* *Argos* starts processing the request, but crashes without logging an error.

The SRE on the squad is the next to suggest a hypothesis: "Maybe CPU usage on the *Argos* server
gets too high and it can't respond?"

You think for a moment before replying, "If that's true, how does it explain the symptoms that we've
observed? How would high CPU utilization lead to these *Vasa* errors?"

"The request would time out because *Argos* would be processing it too slowly."

"Gotcha," you say. "But then aren't we talking about a subtype of the first hypothesis? If there's a
timeout, it means *Argos* crashes before it's done handling the request." The SRE muses on this for
a moment before agreeing.

About ten minutes later, the group has come up with a pretty good list of hypotheses, all of which
are ostensibly testable and explanatory:

1. The web server in front of *Argos* fails to pass certain requests to the service.
2. *Argos* starts processing the request, but crashes without logging an error.
3. *Vasa* can't connect to *Argos* due to a network split.
4. There's a bug in *Vasa* that prevents the request to *Argos* from ever being attempted.

This is a good starting point. You decide to move on the third phase of differential diagnosis:
deciding on some actions to take.

**Next:** [Actions](actions)
