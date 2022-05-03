+++
title = "Exercise 4"
date = 2022-04-26T18:47:49+02:00
weight = 40
chapter = true
pre = "<b>4. </b>"
+++

### Your first orchestrated IoT Process

## Building the Models

You don't actually _have_ to build the models if you don't want to as they are all provided for you here:

- [Exercise 4 Model](exercise4.bpmn)
- [Evaluate Costume Form](evaluate-costume.form)
- [Rate Costume Form](rate-costume.form)
- [Estimate Age Form](estimate-age.form)

You can drag and drop these 4 files into your Camunda Web Modeler to see the models. I've created folders for each exercise, but you don't have to.

![Exercise 4 Folder](/images/exercise4-folder.png)

If you open the `exercise4.bpmn` you will see that all the forms are already linked, and that the `Task Workers` are all filled out as well. We will be re-using the `ScriptTaskWorker` from [Exercise 2](/exercise2) to handle all the 'candy' in this model.

You can now Deploy this model, but don't start a process instance just yet. The IoT Hardware we built in [Exercise 3](/exercise3) will be starting all the instances of this process for us.



