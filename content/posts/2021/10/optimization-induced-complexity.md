---
title: "Nonlinear Effects of Optimization-Induced Complexity"
date: 2021-10-29 07:33:00
tags: [ automation ]
---
_We have school holidays this week, so I'm reposting wonderful comments that would otherwise be lost somewhere in the page margins. Today: Minh Ha on [recent Facebook failure and overly complex systems](https://blog.ipspace.net/2021/10/circular-dependencies-considered-harmful.html#810) (slightly edited)_.

---

I incidentally commented on your NSF post some 3 weeks before [..._the Facebook outage_...] happened, on the unpredictable nature of nonlinear effects resulting from optimization-induced complexity. Their outage just drives home the point that optimization is a dumb process and leads to combinations of circular dependency that no one can account for and test.
<!--more-->
The combinations can be infinite given the parameter space in a large network with lots of features turned on; who has the capability to enumerate all of the twists and turns, let alone test them? Let's face it: tail risks in a complex system aka Black Swan events, by their non-linear nature, cannot be predicted -- think Fukushima -- so instead of trying to rationalize them after the fact, it's much better to go simple in the first place.

Reading the many papers that FB IT Teams published over the years, and one can't help but get the notion that a lot of what these guys do is change for the sake of change. Have to wonder if that's part of their job security? If so, the very same reason is the cause behind the downfall of Big Science, where profit incentive drives people away from doing real science and into shitty career-building and grant-winning parlor tricks. FB IT, including their network teams, always seem to be on the run for one sort of optimization or another -- I suppose the same thing can be said about other HyperScalers as well, and the AGILE movement in general, so this is not directed just toward FB -- but are most of their optimizations optimal or even necessary? I tend to seek out heretic discoveries due to my big distrust of the mainstream, and in one example, [looks like a lot of advanced routing tricks fare no better than plain-old BGP](https://homepages.dcc.ufmg.br/~cunha/papers/arnold19hotnets-bgp.pdf):

So much for optimization. The upside is questionable, while the downside blatantly obvious, exemplified by this outage and the likes. When you cramp too much crap in, at some stage a bifurcation point will be reached, when even a small tiny change will propagate throughout the entire system, causing phase transition and potential collapse, depending on the nature of the change. That is the true Butterfly effect, and not the popular, jaded Butterfly effect people like to brag about in the mainstream. But IT people, being ignorant of this, don't seem to care much about adding complexity on top of complexity, because it makes them look smart.

This, IMO, is one consequence of ****ing around too much with software and computers, of the BS software-eating-the-world mentality. People who spend all day in front of the PC screen lose touch with physical reality, and become stupid nerds thinking all the stuff they read in science fiction can be realized. Over-reliance on technology, attributing non-existent power to it, is a manifestation of this WOKE mentality -- I said over-reliance because look how they couldn't even get into the office after the outage. Maybe making RFC 1925 mandatory reading for all IT workers can be a step in the right direction to help reverse this trend.

As for "_Every large-enough system is full of circular dependencies (someone should make a law out of that)_", see *[How Complex Systems Fail](https://how.complexsystems.fail)*. There's also RFC 3439 that is essentially RFC 1925 BY EXAMPLES. RFC 1925 raises the thesis, 3439 gives it detailed treatment. It is, therefore, a crucial reading that everyone serious about networking must read. Read and re-read, time and time again, to appreciate the lessons in it, and see what a mess the current stage of networking really is.