---
title: Switch case an anti-pattern?
tags:
  - Programming
  - Code smell
---


I have a strong opinion that a switch-case can be a code smell. So when do I consider it a code smell and how can we fix it?

<!-- more -->

The reason a switch-case can be a code smell is that it can also write it as a collection of if-else statements. However, a long list of if-else statements harms readability so we tend to avoid that.

But a lengthy switch-case is often just as hard or even harder to read. The `switch` and the `case` you are inspecting can even be off-screen.

```cs hard-to-read-example.cs
switch(value) {
  // ... snip 300 lines 
  case 5000: {
    value /= 2;
    continue;
  }
  // ... snip 200 lines
  case 2500: {
    value *= 3;
    break;
  }
}
```

And on the other side of spectrum I have seen code that could be replaced with a single line:

```cs way-too-short.cs
switch(value) {
  case "error": throw new Exception();
  default: return value;
}
```

Both examples are of poor quality 