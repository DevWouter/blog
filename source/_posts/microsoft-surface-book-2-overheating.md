---
title: Microsoft Surface Book 2 overheating
tags:
  - Surface Book 2
  - Hardware
date: 2020-05-27 17:23:42
---


When I started my current job, almost 2 years ago, I got issued a Surface Book 2. A more than decent laptop where I needed to be nitpicking to discover any fault at all.

Sadly, half a year ago I started to notice a small performance issue. The laptop would become a bit unresponsive, but I thought nothing of it because the application I was developing was quite big. But over time this problem became worse and worse. Until last month I decided to investigate what was the actual cause of the problem.

So here are a few things I noticed:

1. The CPU would throttle to 400Mhz
2. When I disable hyper-threading (using [throttlestop](https://www.techpowerup.com/download/techpowerup-throttlestop/)) the problem would occur less.
3. When I run a GPU intensive game on the dedicated NVidea GPU (DGPU) the problem didn't occur.
4. The problem can occur simply by opening Firefox and watching a YouTube movie.

At first, it seemed the CPU was overheating, however, the throttling would also occur when the CPU was a cool 60 degrees Celsius. And when a CPU benchmark was running the CPU would throttle but with different characteristics. For example, it would throttle to 1900 or 1200 MHz instead of the 400 MHz I was experiencing.

So "logic dictates" it must be something else then just simply overheating the CPU. The <abbr title="Dedicated Graphics Processing Unit">DGPU</abbr> was also already excluded so it was unclear what the actual cause was.

While watching a Youtube movie the back of the "clipboard" (the detachable screen of the Surface Book 2) became very hot, even though the CPU was cool and had not maxed out for at least an hour. So something was overheating and it was not the CPU.

The answer was the Integrated GPU or IGPU for short.

Whenever a lot of drawing operations (like playing a Youtube movie) were happening the IGPU would max out and this would often (but not always) cause the CPU to throttle to 400 Mhz. And after a bit of testing, I can confirm this seems to be the likely cause. I'm not 100% certain since it doesn't happen all the time. 

Since my warranty is almost expired it will be sent back while I grab another Surface Book 2 from the office. Hopefully, I can confirm that the behavior only occurs on my machine and I can simply reinstall everything on the alternative machine.
