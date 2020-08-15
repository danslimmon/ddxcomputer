---
layout: "page"
title: "Actions – DDx crash course"
permalink: "/crash-course/actions"
---

**Back to:** [Hypotheses](hypotheses)

**Next:** [Putting it all together](putting-together)

The third and final phase of the differential diagnosis cycle is the Actions phase. This is where we
synthesize everything we learned in the Symptoms and Hypotheses phases into a plan.

Generally, the actions we decide to take in this phase will fall into one of two categories:

* **Tests** whose result may falsify one or more hypotheses, and
* **Research** to help the team better understand the problem space.

It's not important to categorize actions as tests or research when we're in the midst of a
troubleshooting session. But differential diagnosis works best when we make sure that there's always
at least one action in progress that can be called a test. Research tasks are great for expanding
the range of hypotheses and symptoms that can be written down, but the way we keep the
problem-solving effort moving forward is by constantly testing and ruling out hypotheses.

```
pragmatic vs. other types of decisionmaking
```

## Example

```
diagram of example network
```

The final phase of the differential diagnosis session has arrived. You and your squad look over the
list of hypotheses that you generated:

1. The web server in front of *Argos* fails to pass certain requests to the service.
2. *Argos* starts processing the request, but crashes without logging an error.
3. *Vasa* can't connect to *Argos* due to a network split.
4. There's a bug in *Vasa* that prevents the request to *Argos* from ever being attempted.

"Okay: given all this, what should we do next?" you prompt.

"I can spend some time looking through customers' error reports and see if the failures have
anything in common that we haven't noticed yet," the support rep offers.

You mull this over. "Sure…" you begin, "but don't go too far down that rabbit hole. If you find some
new symptoms, then great; but remember that there might not be anything left there to find."

You write it down as an action in the doc, making sure to note who's responsible for it:

* [Support] Dig for more correlations between error circumstances

That's a research action, which is all well and good. But, in order to make sure the effort doesn't
stall out, you need to get at least one _test_ action on the books. The SRE on the squad suggests
one: "I can try sniffing network traffic at the boundary between *Vasa* and *Argos* and see what we
see."

"Alright:" you press, "how will that help us rule out some of these hypotheses?" You think you know
the answer already, but you want to make it explicit. At the very least, this will help keep
the group rooted in the DDx mindset. The SRE works out the implications of their suggestion, and you
add it to the actions list:

* [SRE] Sniff traffic at *Vasa*/*Argos* boundary (falsifies hypotheses 1 & 2, or falsifies 3 & 4)

Now you have one test action – an action whose result will falsify at least one hypothesis. This, in
principle, is enough. But the *Vasa* dev has another action to suggest. You add this to the list as
well. At the end of the actions phase, the list looks like this:

1. [Support] Dig for more correlations between error circumstances
2. [SRE] Sniff traffic at *Vasa*/*Argos* boundary (falsifies hypotheses 1 & 2, or falsifies 3 & 4)
3. [Vasa eng] Add a debug log line to *Vasa* that contains more information about the reason that it
   can't complete its request to *Argos* (should falsify either hypothesis 3 or 4)

At this point, you decide to end the meeting. You're off and running.

**Next:** [Putting it all together](putting-together)
