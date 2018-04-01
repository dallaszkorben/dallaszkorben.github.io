---
layout: post
published: true
mathjax: false
featured: true
#imagefeature: cover1.jpg
comments: true
title: Testing Frameworks
modified: '2018-01-03'
description: Introduction of the Testing Frameworks
blog: testing
category: [Testing, Testing frameworks]
tags: [Testing, Testing frameworks]
---
# 1. What is the Testing Framework? Why should I use it?

The Testing Framework is collection of rules, protocols, coding standards, test data handling methods, reporting mechanism for creating and desinging Test Cases. 
Following the guidelines for test automation is not mandatory but doing so provides a lot of benefits.
- Reusability of code
- Maximum coverage
- Low cost maintance
- Minimal manual intervention
- Easy reporting

There are lot of Test Automation Frameworks. They also have benefits and disadvantages. When you build your own Framework you should consider these attributes before you make decision.
In practice a Framework is a combination of the Basic Frameworks for set up to leverage the advantages of some and mitigate the weaknesses of others.

<img src="{{site.url}}{{site.image_folder}}/testing/testframeworks.png" width="900" />

# 2. Linear Automation Framework
With a linear test automation framework, also referred to as a record-and-playback framework, testers don’t need to write code to create functions and the steps are written in a sequential order. In this process, the tester records each step such as navigation, user input, or checkpoints, and then plays the script back automatically to conduct the test.
### Advantages
  - There is no need to write custom code, so expertise in test automation is not necessary.
  - This is one of the fastest ways to generate test scripts since they can be easily recorded in a minimal amount of time.
  - The test workflow is easier to understand for any party involved in testing since the scripts are laid out in a sequential manner.
  - This is also the easiest way to get up and running with automated testing, especially with a new tool. Most automated testing tools today will provide record-and-playback features, so you also won’t need to plan extensively with this framework.

### Disadvantages
  - The scripts developed using this framework aren’t reusable. The data is hardcoded into the test script, meaning the test cases cannot be re-run with multiple sets and will need to be modified if the data is altered.
  - Maintenance is considered a hassle because any changes to the application will require a lot of rework. This model is not particularly scalable as the scope of testing expands.

# 3. Modular Based Testing Framework
# 4. Library Architecture Testing Framework
# 5. Data Driven Framework
# 6. Keyword Driven Framework
# 7. Behaviour Driven Framework