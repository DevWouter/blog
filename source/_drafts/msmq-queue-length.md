---
title: MSMQ missing in computer management 
tags:
    - MSMQ
    - Tech Support
---

So here was a fun thing. While reinstalling a laptop I had to create some MSMQ-queus.
However I had named my laptop `SurfaceBook-Wouter` and because of the extreme length of the MSMQ the queue could not be created as they went over 64 characters.
Even worse, after rebooting, the MSMQ interface in Computer Management would not show since the MSMQ-service could not start.

Fix is easy: Rename the computer 