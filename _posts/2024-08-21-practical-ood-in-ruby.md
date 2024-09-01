---
layout: post
title: Summary for book Practical Object-Oriented Design in Ruby - An Agile Primer
categories: [Book, Blog]
description: Book reading
keywords: Book, Blog
mermaid: false
sequence: false
flow: false
mathjax: false
mindmap: false
mindmap2: false
---

Context: Following the previous blog, I try to find 1 or 2 more books to read so that I won't get boring going through one book.

That's why, I try to pick up a book about it, usually I just ask Reddit or something similar, [reference link](https://www.reddit.com/r/ruby/comments/w0ipu2/book_recommendation_to_start_ruby/). Practical Object-Oriented Design in Ruby: An Agile Primer is also a great book to read.

---

# Chapter 1: Object-Oriented Design

Instead of consider world at a set of events (procedures), we consider the world as an bunch of objects interacts with each other.

A program can be coded however we wants if nothing changes. However, the world is changing, so the code should be able to adapt to the changes. And in order to do that, we need to design the code properly. In order to make programming life easier, design is an important part of the process.

Changing is hard, because of the dependencies. The more dependencies, the harder to change. The more dependencies, the more likely the code will break. In the absent of design, unmanaged dependencies will lead to chaos.

Design is an art of arranging code so that it is easy to change. Part of the difficulty of design is that it is hard to predict the future. The design should be flexible enough to adapt to the changes. 

Practical design does not anticipate future changes, but it does make it easier to accommodate them. The design should be easy to change, and the code should be easy to understand.

-> The purpose of design is to allow you to do design later and its primary goal is to reduce the cost of change.

The tool for design are principles and patterns. Principles are the rules that govern the way we design. Patterns are the common solutions to common problems.

SOLID is a set of principles that help you design well. SOLID stands for:
- Single Responsibility Principle
- Open/Closed Principle
- Liskov Substitution Principle
- Interface Segregation Principle
- Dependency Inversion Principle

Other principles include DRY (Don't Repeat Yourself), Law of Demeter, etc.

There is a correlation between use of good techniques and high-quality code. The principles of good design represent measurable truths and following them will improve the code.

Best way to design is following Agile.

Bad design = Bad code = Technical debt = Slow development = High cost of change = Frustration

# Chapter 2: Designing Classes with a Single Responsibility

Grouping methods into a class, a good easy to changes class would follow TRUE:
- Transparent: The class should tell you what it does.
- Reasonable: The class should do what it advertises.
- Usable: The class should be easy to use.
- Exemplary: The class should encourage others to use it.

Example of a Bicycle, but we define `Gear` as the class, where gear handles multiple responsibilities -> When adding a new feature, we need to change the `Gear` class initialization, and the `Gear` class itself. This is not a good design.

So if a class has many responsibilities, it will have many reasons to change. If a class has only one responsibility, it will only have one reason to change. -> Single Responsibility Principle.

Tip: 
- Make question to the class, if the class can answer the question, then it has only one responsibility.
- Try to describe the class in one sentence, if it has "and" or "or", then it has multiple responsibilities.

Cohesion: The degree to which the elements inside a module belong together. A class with high cohesion is a class that represents a single concept or a single thing.

When to make decision, try to consider future cost, current cost. The "improve it now" vs "improve it later" decision tension always exists. A "good designer understands this tension and minimizes costs by making informed tradeoffs between the needs of the present and the possibilities of the future."

What are tips to write code that can embrace changes:
1. "Depend on Behavior, Not Data"
- Instead of directly using instance variable, use methods to access the data. This way, we can change the data structure without changing the code that uses the data. Can use `attr_reader` to define the method.
- Hide the data structure behind well-defined interfaces. So instead of directly accessing array index, we can hide it behind a method.
2. Enforce Single Responsibility Everywhere
- Try to extract extra responsibilities. For example, if a method traverse the whole array, do things, and return a new array -> we can extract each operation on a member into a separate method. Another example is that if a method does two things, we can extract the second thing into a separate method.
