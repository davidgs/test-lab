---
title: "Creating A Decision Table"
date: 2022-04-26T20:03:28+02:00
draft: false
weight: 10
pre: "<b>A. </b>"
---

### Decision Tables, or DMNN

Of course the Decision Table for this exercise is already created for you, but let's go through and look at it a little bit more in order to understand how it works.

![Decision Table Overview](/images/decision-table-overview.png)

This decision table takes 3 inputs `isCostume`, `Age`, and `Costume Rating` that are used as input to the `Determine Skittles` Decision Table. These are all the variable we need in order to make a determination of how many Skittles to dispense.

If we look at the details of how the decision is made, we can see how these inputs are used:

![Decision Table Details](/images/decision-table-detail.png)

You can see that we first evaluate the rating of the costume and add Skittles (or not) based on that rating. We then evaluate the age of the person, and again add (or subtract) skittles from the total.

In the last step we evaluate the `isCostume` variable and if it is `false`, we zero out the total, because if you're not wearing a costume, you get no candy!

This decision table is a `Collect (sum)` table which means that it will go through all the rules and add up all the values from the rules that apply. It will output the final sum from this table. That's why we save the `isCostume` for last so that we can zero out the total as the last step.