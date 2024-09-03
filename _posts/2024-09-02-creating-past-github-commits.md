---
layout: post
title: Creating "Old" Commits on Github
categories: [Git, Blog]
description: Tips and Tricks
keywords: Tips and Tricks, Git
mermaid: false
sequence: false
flow: false
mathjax: false
mindmap: false
mindmap2: false
---

So after going around and looking at some random people's github profile, I saw that their commit history is so good, and I want to have that too. So I try to find a way to fill in the commit history with some random commits.

![Thy-Pham's github commits](/images/blog/github-commits.png)

So let's explore how this can be done.

# How to create "old" commits on Github

It's actually quite simple, use the following command when you want to create a new commit:

```bash
git commit --date "X days ago" -m "Your commit message"
```

where `X` is the number of days ago you want the commit to be created. For example, if you want to create a commit 10 days ago, you can use:

```bash
git commit --date "10 days ago" -m "Your commit message"
```

# When to use this feature

1. We can use this feature to fill in the commit history with some random commits, which makes the profile looks more professional.
2. We want to adjust the history of the project with commits that are suitable for the project's timeline.

However, I think this feature should be used with caution, as it can be misleading to others if the commit history is not accurate. So use it wisely.