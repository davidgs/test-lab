---
title: "Starting the process"
date: 2022-04-26T20:00:58+02:00
draft: true
weight: 50
pre: "<b>E. </b>"
---

### Starting the Process

The process ID (unless you changed it in the model) is `exercise-5-process`. If you hold down the second button on your camera board for about 10 seconds the board will reset itself and you can repeat the steps from [Exercise 3](../Exercise3/index.md) to configure the board to start the process.

- Enter the WiFi credentials
- Enter your Camunda Platform 8 API Keys from [Exercise 1](../Exercise1/_index.md)
- Save the configuration
- Press the Picture button

If you go back to your Camunda Platform 8 Console now, and look under the Operate tab, you should see your Exercise 5 process running. You can then go to the Task Manager tab to complete the form and watch as the decision table is executed and skittles are dispensed up front.

> **Note:** You can also build and start the go process contained in the Exercise 4 directory by running the following command in your terminal:
>
> ```shell
> $ cd ../Exercise4
> $ go build
> $ ./dispense-candy
> ```
>
> Which will simply build and run the go process. This Go process will print out the number of candy pieces to dispense rather than sending them to the actual Candy Dispenser.