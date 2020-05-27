---
title: Microsoft Surface Book 2 overheating
tags: 
    - Surface Book 2
    - Hardware
    - Problem finding
---

When I started my current job, almost 2 years ago, I also received a brand new Surface Book 2.
And the laptop is perfect. There are some small issues but that is nitpicking that would also apply to any other laptop.

About 6~7 months ago however I started noticing a small issue. It would sometimes become a little bit unresponsive.
This is not uncommon since some of the application that I have been working on could take a quite bit of processing power.

However, over time this problem became worse, until last month I decided to investigate it.

So here are a few things I noticed.

1. The CPU would throttle to 400Mhz
2. When I disable hyper-threading (using [throttlestop](https://www.techpowerup.com/download/techpowerup-throttlestop/)) the problem would not occur.
3. When I run a GPU intensive game on the dedicated NVidea GPU (DGPU) the problem didn't occur
4. The problem can occur simply by opening Firefox and watching a Youtube movie.

My first thought was that the CPU was overheating, however this throttling would also occur when the CPU was a cool 60 degrees Celcius. But when I ran a CPU benchmark the CPU didn't throttle in the same sense as I had seen before. If it did throttle it would throttle to 1200Mhz, but not once did it came near the 400Mhz.

This means that the CPU would sometimes throttle due to something else. I could already exclude the <abbr title="Dedicated Graphics Processing Unit">DGPU</abbr> was not the problem and now I had semi-proof that the CPU wasn't the problem.

There was one thing I noticed though. While watching a Youtube movie the "clipboard" (this is how the detachable screen is called) would become very hot, even though the CPU was cool.

So when I opened Task Manager, I noticed started to notice that the intel GPU would always max out everytime the CPU would throttle. And then I realized that the problem might be the other way around. Whenever the Integrated GPU (aka IGPU) would max out, the CPU would throttle.

So I did some quick testing and this seems to be the case.
I'm not 100% certain if this is the cause, but at least now I can reproduce it realible. It also explains why compiling code would not cause a throttle, but watching Youtube movies does.

There are a few cases were it doesn't behave as I expect and I'm thinking this is because the IGPU uses different processing cores and only one or two might be faulthy. As long as they aren't used, the IGPU seems to work fine. Sadly I don't have any control over it.

So at this point I'm making use of the waranty (which almost had expired) for a replacement. 
At the same time I will be grabbing another machine from the office (same laptop) and see if I can reproduce the problem.
