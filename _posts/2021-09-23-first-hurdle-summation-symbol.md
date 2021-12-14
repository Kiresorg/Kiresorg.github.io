---
layout: post
title:  "The First Hurdle - What is Summation and Why All the Symbols???"
date:   2021-09-23 13:17:11 -0700
categories: jekyll update
---
So I encountered my first hurdle in studying some Computer Science (CS) basics, and not suprisingly, it had to do with a misunderstood symbol.

In the first chapter of Jeff Erickson's book [Algorithms](https://jeffe.cs.illinois.edu/teaching/algorithms/), he used a symbol I've seen often but never really understood:

![Sigma](/assets/img/blog/sigma.png)

This is the Greek letter "sigma", and it corresponds to the English letter "S".

I've often seen it in Excel and other places, and I understood it generally to mean "sum".

In CS, though, it has a much more precise meaning - and after examining it a bit, I'm realizing that it is actually pretty important - and that I kind of already knew what it represented.

In programming, we often have to add up a bunch of numbers. The sigma symbol is just a way to show what we want to add up. Consider this slightly more complex use of the sigma symbol:

![Sigma with numbers](/assets/img/blog/sigma_simple.png)

This represents "let's add the number 2 together 5 times."

Let's explore that a bit more. 

This symbol is actually answering three questions:

1. What number are we going to add together? Here, it's the number 2.
2. What's the amount of this number that we have to potentially add together? Here, it's 5 - so we have five "twos" to work with.
3. Which of that set of numbers will we start with? As in, do we start at the first one, or maybe the second one? Here, we'll start with the first one of the five "twos" we have.

The answer to question one (2) goes to the right of sigma.

The answer to question two (5) goes above sigma.

The answer to question three (1) goes below sigma.

In other words, this whole set of numbers and symbols says, "take five twos and add them together, starting at the first two you have".

This is easily represented in code:

```javascript
let sum = 0;
for(let i = 1; i <= 5; i++) {
    sum = sum + 2;
}
console.log(sum); // 10
```
Now we can really start to understand a slightly more complex use of sigma, like this:

![Sigma with numbers](/assets/img/blog/sigma-array.png)

Here, we are using symbols to represent the answers to our three questions:

1. The collection of numbers is called "a"
2. The amount of items in collection "a" is called "n"
3. The item in collection "a" that we will start our summation with is called "i", and it is set to a value of 1 - that is, we will start our summation with the first item in collection "a"

We see this all the time in code. The only wrinke here is that in most programming languages, collections usually identify their items starting with the number 0 instead of 1; that is, the first item in the collection is item 0.

Here's what that would look like in JavaScript:

```javascript
const a = [2,2,2,2,2];
const n = a.length; // 5
let sum = 0;
for(let i = 0; i < n; i++) {
    sum = sum + a[i];
}
console.log(sum); // 10
```

Here's a diagram that explains it in a bit more formal manner:

![Sigma Notation](/assets/img/blog/sigma-notation.png)


So now I can start to read this CS stuff with a bit more understanding of the math symbols I'll encounter.

I hope this helped you; I can assure you it helped me to work it all out