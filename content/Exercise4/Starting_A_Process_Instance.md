---
title: "Starting A Process Instance"
date: 2022-04-26T19:45:10+02:00
draft: false
weight: 10
pre: "<b>A. </b>"
---

### Starting a Process Instance

Now that we have deployed the model, we can use the Camera to start a process. It's as simple as pressing the second button on your camera board! You should see the bright Flash LED come on and then the camera will take a picture.

This picture will then be sent to a server process (that is running on my cloud server) and that server process will start your process instance with the picture you took.

> **Note:** At the present time there is no mechanism for displaying the picture in-line in your form. This is a current shortcoming of the Camunda Platform 8 Forms implementation but I have submitted a feature request to the Camunda Platform team to have this added. For now, your form will have an uneditable field that contains the complete URL to your picture. You can copy/paste this URL into a new browser tab to see the picture.

If you go to the `Operate` Tab in C8, you should now see a running instance of your process:
