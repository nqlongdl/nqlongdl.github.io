---
layout: post
title: Summary for book The Well-Grounded Rubyist
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

Context: So I have been able to code in Ruby because work requires it, but I found out that most of time, I just:
- Try to find, copy and change a piece of code in the code base with the same functionality that satisfy the product requirement.
- Use ChatGPT / Copilot to helps me finish up the code idea, review code and writing test.
- Haven't fully understand or utilized any great thing about Ruby.

That's why, I try to pick up a book about it, usually I just ask Reddit or something similar, [reference link](https://www.reddit.com/r/ruby/comments/w0ipu2/book_recommendation_to_start_ruby/). One person recommend reading "The Well-Grounded Rubyist", so I thought why don't I give it at try.

So this blog will mostly summarize the content of the book, and try to do as much exercise as possible.

---
# Part 1: Ruby foundations

## Chapter 1: Bootstraping your Ruby literacy

### 1.1 Basic Ruby Language literacy
Ruby is the interpreter, Ruby is the language \
Use irb to mess around \
Identifier tree:
- Variables
  - Local: local variable used in a scope
  - Instance: instance variable of object, prefix with @
  - Class: class variable for class, prefix with @@
  - Global: global variable, prefix with $ \
- Constants: constants follow all cap underscore convention.
- Keywords: stuff like `def`, `if` and `__file__`
- Methods names: follow same rules and conventions as local variables (but can end with `?`, `!`, `=`)

Usually local, instance and class all follow camel_case convention, global follow all caps underscore convention.

Objects are instance of class. \
Object can use methods, for example: `an_object.a_method`. It can be called "sending a message from the right side of dot to the object on the left side of the dot. \
Methods call don't need parentheses if it's called with no params. \
Some methods doesn't need the dot, for example: `puts "Hello"`

Use `puts` to output to stdout \
Use `gets` to input from stdin \
Use `value = File.read("file_name")` to read from file \
Use `file_out = File.new("file_name", "w")` to create a file with the mode w, then we can further proceed with `file_out.puts` or `file_out.print`, and finally, `file_out.close`. This is mostly the same with file operation in other language.

#### Exercises

##### Exercise 1
```ruby
puts "Reading Celsius temperature value from data file..."
num = File.read("temp.dat")
celsius = num.to_i
fahrenheit = (celsius * 9 / 5) + 32
print "Saving result to output file 'temp.out'"
fh = File.open("temp.out", 'w')
fh.puts(fahrenheit)
fh.close
```
##### Exercise 2
```ruby
puts "Reading Fahrenheit temperature value from data file..."
num = File.read("temp.dat")
fahrenheit = num.to_i
celsius = (fahrenheit - 32) * 5 / 9
print "Saving result to output file 'temp.out'"
fh = File.open("temp.out", 'w')
fh.puts(celsius)
fh.close
```

### 1.2 Anatomy of the Ruby installation

Use `irb --simple-prompt -r rbconfig` to starts `irb` with lib `rbconfig`, now use `RbConfig::CONFIG["term"]` to get the needed directory.

`term` could be:
1. `bindir`: Ruby command-line tools
2. `rubylibdir`: provide standard lib like `uri.rb` or `fileutils.rb`
3. `archdir`: files generated from Ruby's C-language extension, compiled into binary. Basically same with `rubylibdir` but works with any architecture because of binary format.
4. `sitedir` and `vendordir`: third-party / code we write / tools download from internet etc.

Use RubyGems to control libs and packages.

### 1.3 Ruby extensions and programming libraries

`load` and `require` to load code up \
`load` can be use multiple times in a file \
`require` (prefer) use to load all features of a file (only once)
`require_relate` is `require` but relative to the file.

### 1.4 Out-of-the-box Ruby tools and applications

We have these tools in Ruby:
- ruby - The interpreter
- irb - The interactive Ruby interpreter
- rdoc and ri - Ruby documentation tools
- rake - Ruby make, a task-management utility
- gem - A Ruby library and application package-management utility
- erb - A templating system

Check each tool reference for more information

## Chapter 2: Objects, methods, and local variables

### 2.1 Talking to objects

Ruby specify in object more than class, when created, an object instance will have a set of methods that declared from a class. However, later on, every object has the potential to "learn" behaviors (methods) that its class didn't teach it.

Usually when defining and calling function, if there is no params, we can exclude the parentheses.

The last line of a function will be the return value (evaluate the expression), every function will return a value. If we want to return in the middle of the function, we need to use the keyword `return`.

### 2.2 Crafting an object: the behavior of a ticket