---
title: Microsoft Surface Book 2 overheating
tags:
  - Surface Book 2
  - Hardware
date: 2020-05-27 17:23:42
updated: 2020-05-28 22:19:00
---

When I started my current job, almost 2 years ago, I received a Surface Book 2. A fitting laptop for a software developer.

Sadly, half a year ago I began to notice a small performance issue. The laptop would become a bit unresponsive and at the time I thought nothing of it as it could be explained by the work I do. But over time this problem became worse. Until last month it became such an annoyance that I decided to fix whatever the problem is.

<!-- more -->

So here is a list of things I noticed:

1. The CPU would throttle to 400Mhz
2. When I disable hyper-threading (using [throttlestop](https://www.techpowerup.com/download/techpowerup-throttlestop/)) the problem would not occur as often.
3. When I run a GPU intensive game on the dedicated NVidea GPU (DGPU) the problem didn't occur.
4. The problem can occur simply by opening Firefox and watching a YouTube movie.

My first assumption was that the CPU was overheating. But that would not explain why the throttle would start when the CPU was still a cool 60 degrees Celsius. And when I would push the CPU to the max using a CPU benchmark it would throttle but with different characteristics. For example, it would throttle to 1900 or 1200 MHz instead of the 400 MHz.

As I was watching a Youtube movie the back of the "clipboard" (the detachable screen of the Surface Book 2) became hot, even though the CPU remained cool. Even more strange the CPU had not done anything intensive for more than an hour. So what was generating this heat?

But I did notice that the Integrated Graphics Processor Unit, or IGPU for short, had maxed out just before the problem occurred. And with some additional testing, I noticed that whenever the IGPU maxed out the CPU would sometimes, not always, throttle to 400 Mhz.

Although not 100% proof, I feel confident that this is the problem. So I have decided to make use of the warranty and grab another Surface Book 2 from the office. 

**Update**: I can confirm that the other Surface Book (with the same specs) does not have the same issue. 
