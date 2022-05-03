+++
title = "Exercise 2"
date = 2022-04-26T18:47:27+02:00
weight = 20
chapter = true
pre = "<b>2. </b>"
+++

### Your First Process

## Implementing a simple script worker in Golang

In Camunda Platform 7 one could choose to implement scripts 'in line' in the process definition. While this was not a 'best practice' and was discouraged for maintainability, it was still a simple option for small problems.

In the original version of the CandyCam project, I used in-line scripts to add Candy to the process at various times. In my defense, I didn't know any better, and it was the easiest way to make it work.

With Camunda Platform 8 SaaS there were no longer any options for inline scripts. Frankly, that's a good thing in my opinion. But it does mean that you have to find a new way to handle these relatively simple tasks. In this exercise we will implement a simple script worker in Golang.

