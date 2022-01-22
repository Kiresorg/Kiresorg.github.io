---
layout: post
title:  "What Should I Know About... CI/CD?"
date:   2022-01-20 13:17:11 -0700
categories: jekyll update
---
# What Should I Know About... CI/CD?

Apparently CI/CD is, like, SUPER important. And everyone should use it, and it will solve all your problems, and if you're not doing it you're either stupid or you just like pain and heartache.

But what exactly is it? And is _any_ of that true?

## Definitions

Right out of the gate, you should know that CI/CD _looks_ like two acronyms (CI and CD), but it's actually _three_ terms:
- Continuous Integration
- Continuous Delivery
- Continuous Deployment

So what do these terms mean? Well, they all revolve around the use of _automation_ - letting a computer program perform actions for you that you might otherwise do manually. The only difference between each lies in _what_ we are automating.

Here are some simple definitions. They may use some terms you don't know yet; we will cover each one as we go along.

> **Continuous Integration**: The use of automation to integrate code changes into a source code repository so that at least one branch is always able to be compiled.

> **Continuous Delivery**: The use of automation to produce an application build package capable of being deployed.

> **Continuous Deployment**: The use of automation to deploy an application.

While these three concepts can be explained simply, there are actually a lot of factors to understand about them, and about the context they're used in. We'll cover all of these factors - some in detail; some just enough to help you grasp what CI/CD is all about.

## Context

### Trust

The basic theory behind CI/CD is this: if the automated systems we use in writing, building and deploying applications create enough trust throughout the organization, we can put our attention on more valuable areas: _faster_ IT service delivery of _safer_ applications to _happier_ customers.

### DevOps

The tools and processes of CI/CD are useful all on their own - but often, companies implement them as part of an overall DevOps strategy or culture.

DevOps, which stands for "Development/Operations", isn't a set of tools or processes - rather, it's a culture. 

It emphasizes rapid delivery of IT services through the adoption of agile, lean practices throughout a company's entire structure. It's all about improving collaboration between "development" (the folks who design, build and test the applications) and "operations" (the folks who host those applications). 

DevOps implementations use technology - particularly _automation_ - to achieve this goal of rapid IT service delivery.

### The Power of Automation

Whether you're looking at CI/CD all on its own or as part of a DevOps culture shift, the primary thing you're looking at is _automation_.  This isn't a novel idea - after all, one of the main reasons we made computers in the first place is to automate things we could do ourselves. 

So when you're trying to understand CI/CD, start with automation - what are we trying to automate, and why?

### So What Are We Automating?

> We're automating the key tasks involved in: writing computer code, turning that code into a computer program that can be deployed, and actually deploying the computer program.

In order to really understand and appreciate CI/CD, you've got to have at least a basic understanding of how software is made. How do we go from instructions a developer writes on a screen, to a running computer program being used by a person or by another computer program?

This is a subject you could study in great detail, but you don't need to for our purposes. Let's just look at the basic series of steps:

1. A developer writes a program in _code_ - instructions written in a human-readable language (like JavaScript or Python, for example).
2. A special program (often called a _compiler_) converts that _source code_ into a form that a computer can actually understand and obey - a form called _machine language_.
3. This set of machine language instructions, called an _executable_ (because it's in a form that a computer can execute), is your actual program. Now we copy it onto a computer where you want it to be used by a person or by another program.

| ![compile.svg](/assets/img/blog/compile.svg) |
|:--:|
| Source code is compiled, resulting in an executable |

### Source Code

There are many different approaches to managing the source code for an application in software development. Most of them make use of multiple "branches" of code, each of which contains a unique version of the text files that make up the application's code. A collection of source code branches for an application is called a repository, or "repo".

There is a lot to know about "source code management" (SCM), and it's another area you should study.

For our purposes, it's enough to know that Continuous Integration works against the branches in an application's repo. More precisely, a CI setup will wait for certain events to occur, at which it will try to automatically integrate an incoming code change into a branch in the repo.

### Where Does All This Automation Happen, Anyway?

Any computer program needs a place to live - an "environment" that contains everything it needs in order to run, so it can provide the service it was designed to deliver. 

There's a lot to know about everything that goes into an application environment, but that's a subject for another time. For now, let's just cover the basics. Here are some of the things _other than your actual computer program_ that you'd need in an environment for that program:
- An operating system
- Any programs your program will need to operate (for example, a web server program)
- Any runtimes needed by your program (runtimes are continuously-running computer programs that let your program interact with the computer's basic functions, like file system access)
- Any database programs your program will need to access as it does its work

All of these parts, and often many others, are part of the environment for your program. Software development makes use of lots of environments.

As an aside, one of the main benefits of "the cloud" is that these environments can be created quickly, on demand - and you can specify their exact configuration.

#### Moving Your Application Through Environments

As a computer program is developed, it goes through several stages. Each stage has its own purpose, but overall, we are trying to get the program closer to our final goal: It is in the hands of our end users, delivering reliable service that makes them happy.

Each of these stages usually needs its own environment - its own complete, functioning system into which you can place your program. While the names of these stages may vary from company to company, they usually follow this sort of sequence:
- Development
- Quality Assurance
- Staging
- Operations

| ![environments.svg](/assets/img/blog/environments.svg) |
|:--:|
| Typical environments for a software application |

<br>
From a big picture point of view, we are moving our program through these environments, so we can do various tasks along the path to a fully-deployed application out in the "Operations" environment (often call "Production" or "Prod").

This is where much of our automation in CI/CD will happen.

## Principles and Theory

### What Are We Automating?
Let's get a little more precise here, and look at _what_ exactly we are automating in each of the three elements of CI/CD.

#### Continuous Integration

As we talked about earlier, Continuous Integration is all about using automation to make sure you've always got at least one branch of the application's code that can be compiled.

> Continuous Integration: The use of automation to integrate code changes into a source code repository so that at least one branch is always able to be compiled.

This ensures the company won't ever be in a position where it can't deliver a working product of some sort.

So what exactly are we automating with CI? _The integration of a code change into a code branch._ We are letting a computer program decide whether or not to allow a change to our code base.

It's important to consider that CI only works with _text files_ - not with a running application. The code base for an application is just a collection of text files, containing instructions written in a human-readable language _that a computer cannot execute_ - so any tasks you automate in this area can only work with those text files. This means you won't be automating things like application startup, feature testing, load testing, etc. - all those tasks require a running application, and at this stage, all we have to work with are text code files.

So in CI, we use automation to create trust by getting the answers to these questions:

- Can the code be compiled?
- Does the code meet any standards we've defined for code quality (formatting, comments, etc.)?
- Does the code pass any static code testing we've defined for it?

> "Static code analysis" is testing you can do on text files. Besides code quality, one very important type of test you _can_ perform on text code files is called "unit testing". Unit tests are unique in that you don't need to create a compiled, executable application in order to run them. Unit testing is another area you should know about.

So if you are going to use Continuous Integration, you'll automate these tasks:

- code compilation
- static code analysis
- unit testing

Put into flowchart form, it might look like this:

| ![ci-flowchart.svg](/assets/img/blog/ci-flowchart.svg) |
|:--:|
| Flowchart for a typical Continuous Integration process |

<br>
Remember, since we are trying to create trust, if errors are encountered during the process the whole effort will be stopped. Needed notifications will be sent out, and conditions will remain as they were before. In this case, that means that the code change that triggered the process will _not_ be entered into the branch of source code.


#### Continous Delivery

This brings us to the next action we can automate: delivery of a potentially-installable version of our application.

> Continuous Delivery: The use of automation to produce an application build package capable of being deployed.

Now that we've verified that we have code that can compile and that meets any static code requirements we've set up, we have a decision to make: will we use automation to actually build the application and deploy it into a working environment, or will we simply build the application and make it available for people to deploy into an environment when they wish?

This is the difference between continuous _delivery_ and _deployment_.

Let's examine continuous delivery. First of all, what are we delivering?

##### The Build Package

What we're going to deliver is called a "build package". It's a collection of several things, all of which are needed if you were actually going to install the application in an environment so you could run the application.

We do this by "building" our application - running a specialized program (a "build agent") that compiles our source code, gathers together needed files, and copies them to a known location. The output of a "build" is called a "build package".

So what might be in a build package?

First of all, you are of course going to have the compiled, executable version of your application - after all, this is what the whole process is about.

There are a number of other items - often called "artifacts" - that might be needed as well. Again, this subject (software builds) is a deep one - but from a high level, here's what else might be in a build package:

- configuration files (text files that contain data your application might need while it's running - things like info on how to connect to a database, or settings for how to handle user authentication, etc.). These files are usually stored in the source code repo, alongside the actual source code files.
- third-party libraries (collections of code, usually centered around specific types of operations) that your program might need while it's running (also called "dependencies", as your application depends on them in order to operate). These are obtained from a trusted source.
- audio/visual assets your application might need.
- log files created during the build process.

So if you are going to use Continuous Delivery, you'll automate these tasks:

- create an executable for the application
- gather any needed dependencies
- gather any needed config files
- gather any needed audio/visual assets
- create and include any specified logs
- put copies of all of these items (artifacts) in a specific location

| ![build-package.svg](/assets/img/blog/build-package.svg) |
|:--:|
| Diagram of the build process |

<br>
Remember, since we are trying to create trust, if errors are encountered during the process the whole effort will be stopped. Needed notifications will be sent out, and conditions will remain as they were before. In this case, that means that whatever previous build package was available will remain available, marked in some way as the most recent trusted build.

#### Continuous Deployment

If we have gotten this far, we have a trusted source code branch which we have used to create a trusted build package for our application. If we want to continue using automation to push the process further, we are in the realm of continuous deployment.

> Continuous Deployment: The use of automation to deploy an application.

It helps to look at what process you would take if you were to manually deploy an application. It might look something like this:

- Make sure you have the build package that was used to deploy the _current_ running version of the application, so you can revert to this if you run into a problem while installing the new build package
- Copy the build package contents to our application's intended environment, overwriting the current files
- Start up the application
- Run tests to verify the new version of the application can be safely left running in the environment
- If the application isn't running properly (won't start up; failed vital tests), use the previous build package to revert (also called "roll back") to the previous set up

So, if you are going to use Continuous Deployment, you'll automate these tasks:

- verify previous build package available
- connect to specified environment and copy build package to specified location
- start application
- run any specified tests
- if tests fail, use previous build package to roll back the environment

## Pipelines, Agents and Workflows

There's another term that is used in a couple of different ways in CI/CD: pipeline. 

A useful definition comes from [InfoWorld](https://www.infoworld.com/article/3271126/what-is-cicd-continuous-integration-and-continuous-delivery-explained.html):

> "Continuous integration (CI) and continuous delivery (CD) embody a culture, set of operating principles, and collection of practices that enable application development teams to deliver code changes more frequently and reliably. The implementation is also known as the CI/CD pipeline.”

So a "pipeline" is the implementation of an idea.

Most of the time when people use the term pipeline, they are talking about a set of items used in automating code integration, delivery and deployment. These items might be:

- Agent: This is the actual computer program that performs automated tasks on your behalf (that's why it's called an agent)
- Workflow: This is a script that specifies the tasks you want automated
- Build machine: This is a computer where the automation work is performed. It's not the place where your application will eventually live; it's the place where the CI/CD work is done
- Environment: This is the place your application will live and run

| ![pipeline.svg](/assets/img/blog/pipeline.svg) |
|:--:|
| Diagram of a pipeline |

## CI/CD Providers and Tools

This system requires a few different service providers in order to work. Here are some of the main types of providers and tools, along with some of the more popular at the time this was written (early 2022):

- Source Control Management (SCM) providers (GitHub; Atlassian Bitbucket; GitLab SCM, etc.)
- CI/CD providers (GitHub Actions; Jenkins; CircleCI; TravisCI; Maven; Atlassian Bamboo; AWS CodeBuild, etc.)
- Scripting language to write workflows (Python; YAML)
- Testing frameworks (Selenium; JUnit; Appium; Cucumber, etc.)

## Bringing It All Together

Here's a one-page summary of the subject:

When you build software, you keep the source code for the software in a repo that has different branches.

Using continuous integration, we can automate the process of making sure one of those branches is always able to be compiled, and that the code meets any quality and unit testing requirements.

Using continuous delivery, we can automate the process of using that code branch to produce a set of files that we could use to install the working software in an environment _if we wanted to_.

Using continous deployment, we can automate the process of actually installing and testing that version of the software in an environment.

The goal is to increase trust in the automation system and in the quality of the tests on your code and the application.

As trust increases, more tasks in the process can be automated and faster application development and delivery can occur.

How it works:

You write a script called a "workflow" that describes the various tasks you want to automate.

In this workflow script, you specify what steps to perform, where to do the work (the build machine), what to do if errors occur, and which environments to deploy the application to (if desired).

A CI/CD provider with access to your source code, your workflow script and your deployment environments watches your source code branch for incoming code changes.

When a code change is submitted, it triggers execution of your workflow script. 

The CI/CD provider starts a program (the "agent"), which attempts to perform the tasks in the workflow script.

As long as these automated actions don't produce fatal errors, the agent continues to execute the specified tasks.

If fatal errors are encountered, the current task is reverted, the workflow is stopped, and notifications are sent out to alert concerned parties.

## Variations on a Theme

One final note to keep in mind if you're sorting out how CI/CD works at your company: sometimes these three terms are used in odd ways.

Nearly any task in this area can be automated, and people can use terminology any way they like. This means you'll see systems with a bit more complexity or nuance than what we've covered, and you'll see terms being used in ways that seem to differ from what we've covered.

The fundamentals we've covered here always apply, and they will help you sort out your specific setup.

As an example, you might find a "Continuous Integration" system that goes beyond simply verifying that the code can compile and that the code meets any code quality/unit testing requirements. Systems exist that, on a code change, actually perform a full build and deployment of the application using temporary environments that mimic the actual environment where the application will eventally live. If this "soft deploy" fails, the code change won't be permitted.

Just remember the basics of this subject and you'll be able to work your way through any CI/CD system.

## Resources

Pluralsight [course](https://app.pluralsight.com/library/courses/devops-foundations-continuous-integration-continuous-delivery/table-of-contents) on DevOps and CI/CD


## Recommended Study

Related areas you should explore:

- DevOps
- Distributed architecture
- Containerization (Docker/Kubernetes)
- Source Control Management
- Unit Testing

## What Else Would You Like To Know About?

I hope this has helped. What other technology subjects would you like to know about? Let me know:

erikdavidtech@gmail.com