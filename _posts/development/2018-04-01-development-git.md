---
layout: post
published: true
mathjax: false
featured: false
comments: true

title: Git
modified: '2018-04-01'
description: Git
blog: development
category: [Development, Git]
tags: [Development, Git]
---
# 1. Data transport and locations

<img src="{{site.url}}{{site.image_folder}}/development/git-datatransport.png" width="500" />

# 2. File status lifecycle

<img src="{{site.url}}{{site.image_folder}}/development/git-filestatuslifecycle.png" width="900" />

# 3. HEAD

HEAD allways refers to the **most recent** commit on the **current branch**.  
When you change branches, HEAD is updated to refer to the new branch’s latest commit.

* **HEAD** refers to the most recent commit
* **HEAD~**, HEAD~1	refers to the commit before the tip
* **HEAD~~**, HEAD~2	refers to the commit even earlier
* **HEAD** = @

In a normal case the HEAD is a symbolic reference to the tip of a branch.  
You can check it with the following example.  
You checkout the master branch and then you check if the HEAD pints to the branch:


