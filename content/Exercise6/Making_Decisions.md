---
title: "Making Decisions"
date: 2022-04-26T19:02:35+02:00
draft: false
weight: 30
pre: "<b>C. </b>"
---

### Making Decisions

Now that we are using a different criteria for our decision, we need to create an entirely new decision table in order to decide how much candy to distribute.

![New DMN Table](/images/NewDMN.png)

Woah! That's a complicated table! In fact, it's not just one table but a whole series of them, all feeding into one final table that will decide how much candy to distribute.

**Note:** the smaller tables contain my proprietary algorithm for giving out candy based on the detected `mood` of the person in the picture but you are welcome to create your own by modifying those tables however you wish.

You can see from the table for `Joy` how I calculate the number of pieces of candy for someone:

![Joy DMN Table](/images/joy.png)

These calculations are entirely made up by me.

Once the number of pieces of candy are calculated for each emotion, the final table adds them all up and provides a final result:

![Final Result](/images/final-result.png)

You can download the [DMN Table](autoskittlesdecider8.dmn) pictured above and deploy it to your Cloud Modeler.

