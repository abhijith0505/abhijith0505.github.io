---
layout: post
title:  "Knowledge from Knowledge Representations"
date:   2022-05-07 02:00:32 +0530
categories: blog
---

I’ve completed an Artificial Intelligence course during my Bachelors and also referred some AI textbooks over the last few years for work. AI, while it does sound fancy and cutting-edge, is a very theoretical subject, even a bit philosophical. But after revisiting those textbooks, I’ve found that **Knowledge Representations** is one particular topic that I really appreciate.


> 💡 The textbook I've referred here is [Artificial Intelligence](https://books.google.co.in/books?id=b4owngEACAAJ)[1].



The representation principle states, “*Once the problem is described using an appropriate representation, the problem is almost solved*”. This, again, sounds theoretical, but hear me out.

In simple words it’s all about how you represent knowledge or data. The representations are frameworks for defining knowledge in a way that you feel fit to solve a problem. You could plan to have it *unstructured* and dump it in a text file somewhere or let it be a simple *relational* representation in some database or CSV file. For more complex needs, you could use *propositional logic*, it could be hierarchical - using a tree perhaps - or even be simply procedural such as If-Else rules (in AI lingo you would call these *Production Rules*).  There’s a bunch of them out there. What is critical is that you pick the right representation that will help your task.

---

### Characteristics of a good representation

Before getting into some of the knowledge representations, here are some of the characteristics of a good representation:

- Make relationships explicit and expose natural constraints
    - If we didn’t have these, then there’s no point using a *knowledge representation.*
- Bring objects and relations together
    - This emphasizes the need to tie them together. Having isolated objects and relations makes it difficult for anyone to draw inferences from it.
- Exclude extraneous details
    - We don’t need to know what we don’t need to know.
- Transparent, concise, complete, fast and computable
    - We’ve got to implement it at the end of the day, so “[KISS](https://en.wikipedia.org/wiki/KISS_principle)”.

Let me try to talk about a couple of knowledge representations I’ve come across. 

### Semantic Networks 🕸️

A Semantic Network is a graphical representation to represent objects and relationship between objects. It consists of nodes, directional links and application specific-labels.

Let’s take a very famous interview question as an example - the [Guards and Prisoner Riddle](https://puzzlefry.com/puzzles/guards-and-prisoners-riddle/)[2]. The problem goes like this:

> There are three guards and three prisoners who need to cross a river. The boat only holds two people at a time, and the prisoners must not be allowed to outnumber the guards on either side of the river; otherwise, the prisoners will overpower the guards and, well, the story will come to an abrupt end. Determine the smallest number of trips to safely transport all of the guards and prisoners across the river.
> 

One way to map this information into semantic networks would be to represent each node in the semantic network by the number of guards and prisoners on either side of the river and the position of the boat. Each node can be imagined to be connected to other nodes using structural links that represents the action taken. This action becomes the semantic label for the network.

With such a knowledge representation in place, any problem solving technique can be used that leverages this. “Generate and Test“ and “*Describe and Match”* are a couple examples - think of it as an algorithm creating new states (nodes) and testing if those states are valid (prune otherwise) and repeat till the solution state is reached. The nodes which don’t lead to the optimal solution is omitted for brevity. This diagram shows that **7** is the optimal number of trips required.

<img src="/assets/2022-05-01/blog.png" width="500">

(Solution state space of the optimal solution using semantic networks.)

A much more harder problem to solve is the Raven’s Progressive Matrices problem. These are the puzzles you usually find in IQ tests.  In short:

> The problems consist of visual geometric design with a missing piece. The test taker is given six to eight choices to pick from and fill in the missing piece. The missing piece will complete the horizontal, vertical and diagonal patterns that exist in the problem.
> 

<img src="/assets/2022-05-01/RPM.png" width="500">

(Example of a Raven’s problem. Image from [wiki](https://en.wikipedia.org/wiki/Raven%27s_Progressive_Matrices).)

<img src="/assets/2022-05-01/agent.png" width="500">

(A complex semantic network representation of a 2x2 RPM-like problem.)


One possible way to construct the semantic network here (as shown in the figure) is by imagining each of the images in the problem to be the node defined by the properties of the image - this could be information such as shape, color, number of objects, etc. The links between images could depict the transformation that happens between images - here, it is the clockwise movement of the black colored component, rotations, and other properties. And, the labels can represent the nature of this transformation, depicted by the key-value pairs.

With this you’ll be able to find the missing image that fits the pattern the best by matching these patterns/relationships (the key-value pairs).

### Frames 🎞️

Frames are another form of (a powerful) representation that behave as molecules - they capture a lot of information compared to other methods (atoms). They have slots and fillers and lets the you generate a stereotype using default values. 

Let’s imagine a problem from Natural Language Processing, a task where a computer program is supposed to read a simple sentence, read a question based on the sentence and answer that question.

Given a sentence like **“Matt and Steve took a green pig to the forest”**, frames enable agents to answer questions like:

- Who was with Matt?
- What did Matt and Steve take to the forest?
- What color was the pig?

Using lexical analysis (fancy way of saying how we find out the parts of speech such as verbs, nouns, etc. from a sentence), we can represent the above sentence using the following Frame representation.

![Frame representation for “**Matt and Steve took a green pig to the forest”**](/assets/2022-05-01/Frames.png)

(Frame representation for “**Matt and Steve took a green pig to the forest”**.)

Now, based on the information extracted from the question, you can easily pick the solution from the frame representation. Say, the question is “**Who was with Matt?”**. If you assign a frame to this question, you’ll find out that Matt is a subject in the question. So, if you look into the subject slot, you’ll find the solution in its filler. Similarly, questions about each of these slots can be answered.

Once you have a well defined knowledge representation in place, the actual strategy of problem solving that you work with will get the other half of the job done. Some knowledge representations could be tightly coupled with certain techniques and some can be loose, general purpose representations, but getting that representation fixed will be crucial for complex AI agent building.

--- 

This year, I started something new, a Masters program from Georgia Tech ([OMSCS](https://omscs.gatech.edu/)). Being one of the most famous online Master's program, you can find plenty of course related information, tips, tricks and what not on the internet. So I intend to start a series championing the topics I learn from the courses I take. [Knowledge-Based AI](https://omscs.gatech.edu/cs-7637-knowledge-based-artificial-intelligence-cognitive-systems/) is the first course I took and the journey has been pretty thrilling so far. I’ll be completing the semester in another week and putting up a review article soon. 

### References

[1] Artificial Intelligence, Winston, P.H., A-W Series in Computer science, 1992, Addison-Wesley Publishing Company

[2] [https://puzzlefry.com/puzzles/guards-and-prisoners-riddle/](https://puzzlefry.com/puzzles/guards-and-prisoners-riddle/)