---
title: MSMQ missing in computer management
tags:
  - MSMQ
  - Tech Support
date: 2020-05-29 18:25:24
---

For an old project we use <abbr title="Microsoft Message Queue">MSMQ</abbr>. But after restarting my computer the MSMQ service would crash at startup. And this also prevents the add-in from appearing in Computer Management. After removing all the `*.mq`-files in `C:\Windows\System32\msmq\storage` and killing/restarting the MSMQ seems to work fine until the computer restarts. So what is causing the problem?

<!-- more -->

As luck would have it, I had documented a recent reinstall of my laptop. Sadly that laptop will be sent away for repairs. So I was using the script to install everything on another laptop. But this time I had added an extra step: I had changed the name of my laptop.

Normally when you install Windows 10 it will give your laptop a random name, which is unpronounceable. So I had renamed this new laptop to 'SurfaceBook-Wouter' and this was causing a problem.

Message queues are supposed to be accessible from the network and so they have the name of the computer in their name. This also applies to private queues. And here is the full name of one of the queues (the name is different but length is an exact match):

```
SurfaceBook-Wouter\private$\theverylongnameofthemessagequeue
```

But when I looked at the documentation of Microsoft ([MSMQQueueInfo.PathName](https://docs.microsoft.com/en-us/previous-versions/windows/desktop/legacy/ms707110(v=vs.85))), I read that some issues might occur if the name is more than 64 characters. But the above name is 58 characters, and I was about to exclude it until I realized that it also creates a longer queue.

When an error occurs the system creates the error queue. Virtually the same as the original, but 'errors' is added to the end of the name. And when a message fails to be processed it will be moved here. And the queue is named:

```
SurfaceBook-wouter\private$\theverylongnameofthemessagequeueerrors
```

And that name is 66 characters. After renaming my laptop to `SB-Wouter` the problem was gone. The name of the error queue would be 57 characters instead of 66. Problem solved!