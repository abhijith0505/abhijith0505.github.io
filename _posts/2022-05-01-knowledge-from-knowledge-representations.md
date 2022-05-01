---
layout: post
title:  "Knowledge from Knowledge Representations"
date:   2022-05-01 02:00:32 +0530
categories: blog
---

This year, I started something new, a Masters program from Georgia Tech ([OMSCS](https://omscs.gatech.edu/)). Being one of the most famous online Master's program, you can find plenty of course related information, tips, tricks and what not on the internet. So I intend to start a series championing the topics I learn from the courses I take. [Knowledge-Based AI](https://omscs.gatech.edu/cs-7637-knowledge-based-artificial-intelligence-cognitive-systems/) is the first course I took and the journey has been pretty thrilling so far. I’ll be completing the semester in another week and putting up a “review” article for anyone that would be interested in that. I’ve completed an *Artificial Intelligence* course during my Bachelors and also referred some AI textbooks over the last few years for work. Some of us would agree that AI, while it does sound fancy and cutting-edge, is a very theoretical subject, even a bit philosophical. But after revisiting those textbooks again during this course, I’ve found that **Knowledge Representations** is one particular topic that I’ve started to appreciate more.


> 💡 The textbook I've referred is [Artificial Intelligence](https://books.google.co.in/books?id=b4owngEACAAJ)[1]. You’ll find most of the details scraped from there.



The representation principle says, “*Once the problem is described using an appropriate representation, the problem is almost solved*”. This, again, sounds theoretical, but here me out.

### Characteristics of a good representation

Before getting into some of the knowledge representations, here are some of the characteristics of a good representation:

- Make relationships explicit and expose natural constraints
    - If we didn’t have these, then there’s no point using a *knowledge representation.*
- Bring objects and relations together
    - This primarily emphasizes the need to tie them up together. Having isolated objects and relations makes it difficult for anyone to draw inferences from it.
- Exclude extraneous details
    - We don’t need to know what we don’t need to know.
- Transparent, concise, complete, fast and computable
    - We’ve got to implement it at the end of the day, so “[KISS](https://en.wikipedia.org/wiki/KISS_principle)”.

Let me try to talk about a couple of knowledge representations I’ve come across in the course and how useful it can be. 

### Semantic Networks 🕸️

Semantic Networks is a graphical representation to represent objects and relationship between objects. It consists of nodes, directional links and application specific-labels.

Let’s take a very easy and famous interview question as an example - the Guards and Prisoner Riddle. So the problem goes like this:

> There are three guards and three prisoners who need to cross a river. Their boat only holds two people at a time, and the number of prisoners must not be allowed to outnumber the number of guards on either side of the river; otherwise, the prisoners will overpower the guards and, well, the story will come to an abrupt end. Determine the smallest number of trips to safely transport all of the guards and prisoners across the river.
> 

For this problem, each node in the semantic network is defined by the number of guards and prisoners on either side of the river and the position of the boat. Each node can be imagined to be connected to other nodes using structural links that represents the action taken. This action becomes the semantic label for the network.

The diagram shows how the semantic representation of this problem would look like.  The nodes which don’t lead to the optimal solution is omitted for brevity. This diagram shows that **7** is the optimal number of trips required.


![blog.png](/assets/2022-05-01/blog.png)

With such a knowledge representation in place, any problem solving technique can be used that leverages this. Generate and Test and *Describe and Match* are a few examples.

This is a very trivial problem, and one could question the necessity of thinking on the lines of knowledge representations to solve this. That’s just to explain the concept.

A much more harder problem to solve is the [Raven’s Progressive Matrices](https://en.wikipedia.org/wiki/Raven%27s_Progressive_Matrices) problem. These are the puzzles you usually find in IQ tests.  In short:

> The problems consist of visual geometric design with a missing piece. The test taker is given six to eight choices to pick from and fill in the missing piece. The missing piece will complete the horizontal, vertical and diagonal patterns that exist in the problem.
> 

![Example of a Raven’s problem. Image from [wiki](https://en.wikipedia.org/wiki/Raven%27s_Progressive_Matrices).](/assets/2022-05-01/RPM.png)

(Example of a Raven’s problem. Image from [wiki](https://en.wikipedia.org/wiki/Raven%27s_Progressive_Matrices).)

One possible way to construct the Semantic Tree here is by imagining each of the image in the problem to be the node defined by the properties of the image - this could be information such as shape, color, number of objects, etc. The links between images could depict the transformation that happens between images - here, it is the clockwise movement of the black colored component. And, the labels can represent the nature of this transformation. 

With such a representation, the agent will be able to infer what transformation would be required for the final (solution) image and what it would look like. This enables the agent to simply compare the options that it available to this representation to pick the right solution.

### Frames 🎞️

Frames are another form of (a powerful) representation that behave as molecules - they capture a lot of information compared to other methods (atoms). They have slots and fillers and lets the agent generate a stereotype using default values. 

Let’s imagine a use case from Natural Language Processing, a task where an agent is supposed to read a simple sentence, read a question based on the sentence and answer that question.

Given a sentence like **“Matt and Steve took a green pig to the forest”**, frames enable agents to answer questions like:

- Who was with Matt?
- What did Matt and Steve take to the forest?
- What color was the pig?

Using simple lexical analysis, we can break down the sentence into nouns, verbs, adjectives, and so on. Using these features, we can represent the above sentence using the following Frame representation.

![Frame representation for “**Matt and Steve took a green pig to the forest”**](/assets/2022-05-01/Frames.png)

(Frame representation for “**Matt and Steve took a green pig to the forest”**.)

Now, based on the information extracted from the question, the agent can easily pick the solution from the frame representation. Again, a trivial example, but you should be getting the idea.

Once you have a well defined knowledge representation in place, the actual strategy of problem solving that you work with will get the other half of the job done. Some knowledge representations could be tightly coupled with certain techniques and some can be loose, general purpose representations, but getting that representation fixed will be crucial for complex AI agent building. 

### References

[1] Artificial Intelligence, Winston, P.H., A-W Series in Computer science, 1992, Addison-Wesley Publishing Company

[2] [https://puzzlefry.com/puzzles/guards-and-prisoners-riddle/](https://puzzlefry.com/puzzles/guards-and-prisoners-riddle/)