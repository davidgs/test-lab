---
title: "Testing"
date: 2022-04-26T19:04:33+02:00
draft: false
weight: 30
pre: "<b>B. </b>"
---

### Testing your Script Worker

To make sure that your script worker is working correctly, let's run a few tests.

First, we will need to create and deploy a process that will call your script worker task.

in the [`script-worker.go`](../setup/script-worker.go) file set the `PROC_NAME` constant to `AddOneTask`, build and start your `script-worker`.

There is a file [`test-script-worker.bpmn`](test-script-worker.bpmn) in this directory that you can use to create a test process. You can drag-drop this file into the Modeler tab of Camunda Cloud. Your process should look like this:

![Test Script Worker Process](/images/test-script-worker.png)

You can click the `Deploy Diagram` button to deploy the process. Once the process is deployed, click the `Start Instance` button to start a process instance.

If you've made no changes to the process diagram, your process should complete very quickly. You can go to the `Operate` tab and see a list of processes that are running (or finished).

![List of finished processes](/images/process-list.png)

If you click on the process ID in the list, you can see that the process has completed, and that the total count at the end is `10`. (We started it with `count=0` and added `add=1` to it, then added `4`, then added `5`.)

Alternatively, we could start the process with an arbitrary number, and add any number to it in the first step. To do this, we add a starting set of variables to the process:

```json
{
  "count": 10,
  "add": 5
}
```

![Starting process with arbitrary variables](/images/variables.png)

And we will end up with a final count of `24` (10 + 5 + 4 + 5 = 24).

![Final count](/images/final-answer.png)

We will be using this simple script-worker for other parts of this lab.
