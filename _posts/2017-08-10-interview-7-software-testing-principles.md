---
layout: post
published: true
mathjax: false
featured: true
#imagefeature: cover1.jpg
comments: true
title: 7 Software Testing Principles
modified: '2017-08-10'
description: Interview questions-7 Software Testing Principles
categories:
  - Interview questions
tags: [Interview questions]
---

If you were to test the entire possible combinations project EXECUTION TIME & COSTS would rise exponentially.
We need certain principles and strategies to optimize the testing effort.

# 1. Exhaustive testing is not possible
we need `optimal amount of testing` based on the risk assesment of the application.

How do you determine the risk? This brings to the next principle.

# 2. Defect Clustering
The Pareto principle (20-80 rule) originally came from the economy but it is valid in different areas of the life.
For many events, 80% of the effects come from 20% of the causes.
To Software Testing: `80% of the problems are found in 20% of the modules`.
With experience you can identify such risk modules.

!BUT! This approach has it own problem: 
If the same test are repeted over and over again, eventually the same test cases will no longer find new bugs.

# 3. Pesticide Paradox
Repetitive use of the same pesticide lead to the insects developing `resistance` to the pesticide.
Same set of repetivive tests will be useless for discovering new defects.
To overcome this, the test cases need to be regularly reviewed and revised, adding new, different test cases.

# 4. Testing shows presence of defects
!but! cannot prove that there are no defects.
So the Testing reduces the probability of undiscovered defects remaining in the software 
but it is `not a proof of correctness`.

This leads us to the next principle.

# 5. Absence of Error
Just because testing didn’t find any defects in the software, it doesn’t mean that the software is `ready to be shipped`.
Finding and fixing defects does not help if the system build is unusable and does not fulfill the user's needs & requirements.

To solve this problem, the next principle of testing states that Early Testing.

# 6. Early Testing
Testing should start `as early as possible` in the Software Development Life Cycle. 
The later you found the defect the more expensive.

# 7. Testing is context dependent
The way you test an e-commerce site will be different from the way you test a commercial off the shelf application. 
You might use a `different` approach, methodologies, techniques and types of testing depending upon the application type.
