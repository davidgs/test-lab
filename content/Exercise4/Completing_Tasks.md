---
title: "Completing Tasks"
date: 2022-04-26T19:44:45+02:00
draft: false
weight: 20
pre: "<b>B. </b>"
---

### Completing Tasks

Now that the process has been started by your picture, you can go to the Task List tab in Camunda Platform 8 where you should now see a new Task:

![Exercise 4 Task List](/images/exercise4-task-list.png)

You will need to click the `claim` button in order to be able to make a selection on if this is a picture of a person in a costume or not.

Once you click the `Complete Task` button the task will disappear from your task list. If you go back to your `Operate` Tab you can see the token moving along the diagram. The path that it has taken so far will be highlighted in blue.

![Exercise 4 Task List](/images/exercise4-task-list.png)

You will now need to go back and forth between the `Operate` Tab and the `Task List` Tab to see the process move along the diagram as you complete the tasks in the Task List.

At the end, you should hear Skittles come out of the dispenser at the front of the room.

> **Note:** You can also build and start the go process [dispense-candy.go](dispense-candy.go) contained in this directory by running the following command in your terminal:
>
> ```shell
> $ go mod init dispense-candy
> $ go mod tidy
> $ go build
> $ ./dispense-candy
> ```
>
> Which will simply build and run the go process. This Go process will print out the number of candy pieces to dispense rather than sending them to the actual Candy Dispenser.
