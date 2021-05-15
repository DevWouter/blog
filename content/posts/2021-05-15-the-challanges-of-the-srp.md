---
title: "The challenges of the Single Responsibility Principle"
date: 2021-05-15T23:12:14+02:00
draft: false
---

In my opinion, the SRP is one of the most famous software design principles that due to widespread misunderstanding is used wrong causing a decrease in the quality of the code.

Most people have heard of SOLID, an acronym invited by Robert C. Martin. And the majority of them also know that the "S"  stands for the Single-Responsibility Principle, which for the sake of this article I will shorten to SRP.

To quote Wikipedia:

> The single-responsibility principle (SRP) is a computer-programming principle that states that every module, class, or function in a computer program should have responsibility over a single part of that program's functionality, and it should encapsulate that part.

Applying it correctly comes down to two problems.

## Not understanding functional behavior

The first problem is that most developers are good at defining the technical behavior of their code but terrible at defining the functional behavior of their code. If you don’t understand the difference the easiest way is thinking of ordering at a fast-food restaurant.

When you want to eat, you order a meal. Which is your functional behavior. But your technical behavior is that you go walk up to the counter, look at the menu, list the elements of the meal you wish delivered, no, you don’t want the extra of the month.

Imagine you have had your meal and decided you still want a dessert. Do you tell your friends at the table your functional behavior or your technical behavior? Unless you enjoy trolling your friends you will most likely tell them you will "get a desert" and not that you will walk to the counter, tell them you want ice cream, pay, wait, receive ice cream and return to your seat.

Now you might this doesn't apply to you. You would never do that. But if I ask you to explain some recently written code would you use more or less than 8 words? Because if it's more than you are most likely giving me a technical description instead of a functional one.

The reason why I asked for recently written code is that we forget the technical behavior of code over time and as such don't make that mistake.
Not understanding what a module is
The second problem is the "module" part, which we often skip. A module is just another way of saying "application" or "library". Because of our focus on class and methods, we often avoid the easy examples for SRP.

For example, a calculator is used for calculating numeric values, you can’t write code with it and you can’t use it to spellcheck an article. Now you might be one of those who has a fancy graphical calculator which allows writing code and given enough time you might be able to write an application that can be used to spellcheck an article.

But before you do that can I suggest you grab a computer (or even your phone), download a modern text editor, and use that. Because I can guarantee you one thing: Spellchecking using a modern text editor will provide you with a better experience than using a graphical calculator.

And that’s what SOLID is all about: Using software designs to write code that is understandable, flexible, and maintainable.

## How to apply SRP using classes and functions

With the above example, SRP is clear for everyone when writing an application or library. But when we write classes or functions it becomes harder. To apply SRP in a functional manner you need to be able to define the functional element of that piece of code.
Since providing a good example is hard, I will give you quite two bad examples of SRP.

1. _"This class uploads and downloads data, so that are two responsibilities and should be separated."_  
    This is not breaking SRP, the function of the class is to communicate with the server.

2. _"This function writes text to the screen and asks the user for input, so that are two responsibilities and should be separated."_  
    This is not breaking SRP, the function of the method is for the user to answer a question.

Both of these examples have happened to me. In both cases, the developer was explaining the technical behavior and not the functional reason: Communicating data with an external service and interaction with the user.

In some instances, the functional behavior is the same as technical behavior. For example, the minus functions subtract one number from another.

## The easy fix

Robert C. Martin has created an awesome acronym (SOLID and SRP) which when applied correctly improves the quality of your code. However, applying it incorrectly will drastically reduce the quality of the code.

The fix is easy: Instead of talking about "single responsibility" answer the question of what the consumer (either another developer or user) is trying to achieve without using technical terms.

- As a consumer of this application, I want to write an article without spelling mistakes
- As a consumer of this class, I want to get the latest version from the server
- As a consumer of this function/method, I want the user to provide an answer to a question

Once you starting thinking in functional elements SRP makes a whole lot more sense and the quality of your code will improve.