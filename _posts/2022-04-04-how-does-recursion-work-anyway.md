---
layout: post
title:  "How Does Recursion Work Anyway?"
date:   2022-04-04 00:17:11 -0700
categories: jekyll update
---

# What is Recursion and How Does it Work?

Okay, so I’m going to try to explain recursion in a simple way. 

In order to understand recursion, you first need to understand these concepts:

- path of execution
- sub-program
- execution context
- call stack

## Path of Execution
Computer programs are essentially a series of sequential instructions, performed (or executed) by the computer.

This sequence is called the "path of execution".

Programs will have a "main" path of execution - the one that starts with the first instruction in the program, and ends with the last.

Along the way, as this series of instructions is performed  (the main execution path), we may need to call upon smaller sets of instructions that are designed to be used when needed. 

This brings us to sub-programs.

## Sub-programs
These are essentially small programs, with a series of instructions that are executed in sequential order - just like those in the main execution path.

Depending on the programming language used, these may be called subprograms, or functions, or methods - or some other term. The concept remains the same: these are small programs that can be used as needed to perform tasks that the main program may need from time to time as it runs throught the main execution path.

From this point on, we'll use the term "function" to refer to this sub-program concept.

The action of asking one of these functions to do its work is referred to as "calling" the function.

## Execution context
Computers can only execute one instruction at a time. The current series of instructions being performed is called the "execution context" - it is where the focus of the computer is currently placed.

When a computer program starts, the execution context is in the main execution path.

If a function is called from the main execution path, the context now shifts to the execution path inside the called function. Once that execution path is completed, the context returns to the main execution path.

The same principle applies if one function calls another function - while that second function is being executed, context shifts to it. When that second execution path is completed, context returns to the first function. When that execution path is completed, context returns to wherever the context was when that first function was called.

## The call stack
The computer keeps track of function calls in a list called the "call stack".

When a function call is made, that call goes on the list. It stays on the list until the path of execution in the called function is completed. At that point, the call is removed from the list, and context returns to the execution path where the function was called.

It is entirely possible that one function will call a second function before the first is done executing. In this case, both calls will be on the call stack.

The call stack operates on a "First In, Last Out" principle. This means that each successive call is placed at the top of the list, and the top call is the first one that can be removed. 

This means that, where there are multiple calls in the stack, the most recent one must be completed before any previous calls can be completed.

### **Super Ultra Important Point if You Ever Want to Understand Recursion**
Before we move on, I want to make one point - a point that is CRITICAL to understanding recursion:

**EVERY CALL TO A SPECIFIC FUNCTION IS A SEPARATE ACTION BY THE COMPUTER, AND IS TRACKED SEPARATELY BY THE COMPUTER.**

This means you can have two function calls, each to the *same function*, each of them running at the same time. Each call is on the stack, with the most recent being placed above the one immediately prior.

While the *name* of the function being called is the same in each case, the two function calls have *nothing to do with each other* - they are each separate actions as far as the computer is concerned.

You can think of each function call as a separate "mini-program", being tracked by the computer. The actions in one are not related to the actions in another, and the *data* in one is not related to the data in another.

We will come back to this point - which is, I stress again, super important in understanding recursion.

## Recursive functions
We have covered these concepts:
- path of execution
- sub-program
- execution context
- call stack

Now let's look at recursion.

> Recursion is the action of calling a function that will, in turn, call itself.

> This can happen multiple times. Each such call is added to the call stack.

> This stack of function calls will continue until some specific condition, checked in each function call, is met. This condition is called the "base case".

> Once the base case is met, the function call *in which it is met* can complete - at which point it comes off the stack.

> The computer then revisits each previous function call, completing any instructions not yet performed and removing the call from the stack as it completes.

> Once all function calls have completed, the recursive action itself is complete.

### Iterative approach vs. recursive approach
Any action you perform in this manner can also be performed in an iterative manner (using a ```while``` loop or a ```for``` loop, for example).

Let's examine how we'd approach a problem with an iterative approach; then we'll look at approaching the same problem with a recursive approach.

Since it’s used so often in recursion, let’s take up the problem of calculating the *factorial* of a given number.

It may have been a while since you studied factorials in mathematics, so here's a refresher:

> The *factorial* of a given number is the result of multiplying the whole numbers (no fractions) in a set of numbers. 

For example: the factorial of 5 would look like this:

```
5x4x3x2x1 = 120
```

If you have any confusion on this, please take your time and do the math.

Okay, let's move on.

#### Iterative solution

Let's solve this with an iterative approach - a ```for``` loop:

```javascript
function getFactorialWithLoop(n) {
	let result = 1;
	if (n > 1) {
		for (let i = 1; i <= n; i++) {
			result = result * i;
		}
		return result;
	}
	else {
		return "n has to be positive";
	}
}

console.log(getFactorialWithLoop(5));
// output: 120
```

Use a JavaScript editor to write and run this code. The output should be 120.

#### Recursive solution
Now let's approach this same problem with a recursive approach.

A recursive approach works like this:
- We identify the core data processing task we want to use in solving a problem.
- Then we apply that task to the problem some number of times, each time reducing the size of the task.
- When we have reduced the size of the problem such that the core task doesn't need to be performed any longer, we can stop reducing
- We take the work of each previous task up in turn
- The combined work of each application of the task ends up being the overall solution to the task.

Let's use that approach to work out what we need to do to solve factorials in a recursive manner:

> The problem: We need to calculate the total result of multiplying each whole number in a set of numbers, where the set starts at some positive number and contains all positive whole numbers less than that number.

> The "core data processing task" we want to use in solving the problem: Multiply a number by the whole number that is one less than itself:
```
x = y x (y-1)
```

Let's examine what this would look like for calculating the factorial of 3.

We can write it out like this (note that the exclamation point is used here to represent the factorial operation):

```
!3 = 3 x 2 x 1
!3 = 6
```

Remember that we are going to apply the "core data processing task" to reduce the size of the problem.

The first time we apply this task, we multiply 3 times 2.

The size of our problem has now been reduced - all that is left is to take the result of our first task and multiple it by 1.

So we then do that action, multiplying our previous result (6) by 1.

At this point, the size of our problem is such that our task no longer needs to be performed - we've run out of numbers to be multiplied.

Our recursive action can now be completed, with the work of each task being combined to give us the overall result of our work - the total of 6.

Let's build this out in code.

A recursive function will look like this, in pseudocode:

```javascript
function recursiveFunction(parameter) {
	if(parameter equals exitCondition) {
		return parameter;
	}
	else {
		// modify parameter in some way
		return recursiveFunction(modifiedParameter);
	}
}
```

In general, a recursive function has two parts:
- a *base case* (the situation in which our work is done, as the overall problem has been fully reduced); and 
- a recursive step (our "core data processing task")

In a recursive function, we always check the base case first - we need to see whether or not we even need to perform the recursive step. In the pseudocode above, this is the lines
```javascript
if(parameter equals exitCondition) {
	return parameter;
}
```

The "core data processing task" is the lines
```javascript
// modify parameter in some way
return recursiveFunction(modifiedParameter);
```

Here is a recursive function to calculate factorials:
```javascript
function getFactorialRecursively(n){
	if (n <= 1){
		return 1;
	} else {
		return n * getFactorialRecursively(n-1);
	}
}

console.log(getFactorialRecursively(3));
// output: 6
```


Here, the base case is arrived at when the whole number we are addressing is <= 1. This means the problem has been reduced such that no further processing is needed. When we arrive at this point, we can stop executing code in the current function call by returning that lowest possible whole number to the function call immediately prior.

The code for our base case is:
```javascript
if (n <= 1){
	return 1;
}
```

Let's examine the "core data processing task" - the recursive function call itself:
```javascript
return n * getFactorialRecursively(n-1);
```

Here, we are trying to do math. Specifically, we want to multiply the value of ```n``` *as it exists in the current function* by *the value we will get if we call the recursive function while passing in the whole number that is one less than the current value of ```n```*.

This code is best understood by going through it step by step.

### Step-by-step walkthrough
The first actual function call we make is to the built-in JavaScript function ```console.log()```. 

That function can't complete until the function call inside its parentheses is complete - so the function call gets added to our stack.

Our stack now has one call on it:
```javascript
console.log()
```

Look at the first call to ```getFactorialRecursively()```. Let's say we are passing in the whole number 3, just as in the above code.

We call that function.

The function call gets added to the stack.

Our stack now has two calls on it:
```javascript
getFactorialRecursively(3)
console.log()
```

We enter the function call ```getFactorialRecursively(3)```.

We check the base case. As 3 is greater than 1, we continue into the ```else``` block.

In that block, we want to multiply 3 by whatever we will get as a return when we call ```getFactorialRecursively()``` again.

This time, though we are going to call ```getFactorialRecursively()``` with the value 2 passed in as a parameter - since 3 minus 1 is 2.

THIS NEXT PART IS VERY IMPORTANT!

Right now, we have two function calls on the stack - the call to ```console.log()```, and the call to ```getFactorialRecursively(3)```. NEITHER FUNCTION CALL HAS COMPLETED EXECUTION, so they stay on the stack.

The ```getFactorialRecursively(3)``` call can't complete, as it is waiting for a value to come back from the next call to ```getFactorialRecursively()``` - the one we are about to make.

And the ```console.log()``` call can't complete, as it has not gotten a value returned to it by the first ```getFactorialRecursively()``` call.

So, we make that function call to ```getFactorialRecursively()```, passing in the value 2.

That function call gets added to the stack, above the most recent function call.

Our stack now has three calls on it:
```javascript
getFactorialRecursively(2)
getFactorialRecursively(3)
console.log()
```

Now we're inside this new function call.

We check the base case. Nope, 2 is greater than 1 - so we continue into the else block.

We again want to do math. Specifically, we want to multiply 2 by whatever we will get as a return when we call ```getFactorialRecursively()``` again.

Okay, we are about to make yet another call to ```getFactorialRecursively()```.

We do so, passing in the value 1 as a parameter (becaue 2-1=1).

Remember, this call *also* gets added to the stack. We now have *four* calls on the stack:

```javascript
getFactorialRecursively(1)
getFactorialRecursively(2)
getFactorialRecursively(3)
console.log()
```

None of these function calls is complete.

So, let's see what happens when we run through the code in this latest call to ```getFactorialRecursively()```:

We check the base case. NOW we meet the base case - the number passed in as a parameter was 1.

We have now reduced the initial problem to its smallest size - there are no more numbers to process, as factorials only work with positive whole numbers.

Per the logic in our base case code block, we return the value 1 to the previous function - and we REMOVE THE CURRENT FUNCTION CALL FROM THE STACK, as it is done executing.

Our stack now has only three calls on it:
```javascript
getFactorialRecursively(2)
getFactorialRecursively(3)
console.log()
```

Context for the computer is now returned to the previous function call, the one now at the top of the stack.

As the function we were just in returned a value, 1, we can complete our math operation.

Remember that in this function call, the value of ```n``` is 2 - so our math results in a value of 2 (2x1=2).

We return that value to the previous function call, and we REMOVE THE CURRENT FUNCTION CALL FROM THE STACK.

Our stack now has only two calls on it:
```javascript
getFactorialRecursively(3)
console.log()
```

Context for the computer is now returned to the previous function call, the one now at the top of the stack.

As the function we were just in returned a value, 2, we can complete our math operation.

Remember that in this function call, the value of ```n``` is 3 - so our math results in a value of 6 (3x2=6).

We return that value to the previous function call, and we REMOVE THE CURRENT FUNCTION CALL FROM THE STACK.

Our stack now has only one call on it:
```javascript
console.log()
```

Since the previous function returned a value, 6, we can complete the ```console.log()``` call. We do so, resulting in a console output of the number 6.

We then remove that call from our stack - and our stack is empty.

Our main program is now able to continue with any further instructions in the main execution path.

There you have it - recursion in action.

### When should I use recursion?
Recursion is made for solving problems that can be broken down into smaller, repetitive problems. It is especially good for working on things that have many possible branches and are too complex for an iterative approach.

A typical use case for recursion might be searching through a file system. Folders and files are not held to a strict structure, and folders can contain nothing, only files or folders, or both files and folders. Designing an interative function to search such a structure would be very hard, and the code would be hard to follow.

Instead, you could design a recursive function that would keep drilling down into a path of folders and files until there wasn't anything left unexamined, and then go back up the structure to find another path it hadn't searched. The function would search that path in turn, in a similar manner. Once all paths had been searched (the base case), the function would be complete.

Here is an example of such a function, designed for execution on a server using Node.js. It makes use of a Node library called "fs", which provides built-in functions for working with file systems. It also makes use of a Node library called "path", which makes it easier to work with exact paths to folders and files.

```javascript
const fs = require("fs")
const path = require("path")

const getAllFiles = function(dirPath, arrayOfFiles) {
  files = fs.readdirSync(dirPath)

  arrayOfFiles = arrayOfFiles || []

  files.forEach(function(file) {
    if (fs.statSync(dirPath + "/" + file).isDirectory()) {
      arrayOfFiles = getAllFiles(dirPath + "/" + file, arrayOfFiles)
    } else {
      arrayOfFiles.push(path.join(__dirname, dirPath, "/", file))
    }
  })

  return arrayOfFiles
}
```

Other common situation where recursion is helpful is in processing other tree data structures like the file system above, or in processing graph data structures (such as a model of social media connections).

## Conclusion
I hope this helped remove any mystery or confusion from recursion. Let me know your thoughts.