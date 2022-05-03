---
title: "Setup"
date: 2022-04-26T19:04:26+02:00
draft: false
weight: 20
pre: "<b>A. </b>"
---

### Seting up the Worker

The [`script-worker.go`](script-worker.go) file is the solution here. It will start a task worker and listen for tasks from your process. When a task is received, it will execute the task and then complete the task.

The task listener looks for 2 variables in the incoming job: `count` and `add`. If the `count` variable is missing, it will default to initializing it at 0. If the `add` variable is missing, it will default to adding 1 to the `count` variable.

In order to communicate with the Camunda Platform 8 (C8) service, we need to initialize all of the required variables like `ClientID`, `ClientSecret`, etc. In order to do this you can either set environment variables or fill out the `zeebe.yaml` file to hold the values:

```yaml
zeebeAddress: 'YOUR_SERVER_ADDRESS.bru-2.zeebe.camunda.io:443'
zeebeClientID: 'YOUR_CLIENT_ID'
zeebeClientSecret: 'YOUR_CLIENT_SECRET'
zeebeAuthServer: 'https://login.cloud.camunda.io/oauth/token'
```

We will use this file throughout this workshop, so I suggest putting it at the top-level of your project.

The `script-worker` process will read this file in and set all the variables as needed to communicate with the C8 processes.

The only edit to the Go file that is required is to change the `PROC_NAME` constant to the name of your process.

```go
// Set this to the name of your task
const PROC_NAME = "AddOneTask"
```

Once this is set you can start the `script-worker` with the following commands:

```bash
$ go build
$ ./script-worker
```

When you start processes in Camunda Platform 8 that call your `PROC_NAME` task worker, you should see output like this:

```shell
Starting Camunda Cloud Zeebe ScriptWorker
===================================
handleC8Job
{Add:0 Count:0}
{Add:1 Count:1}
Complete job 4503599627617096 of type AddOneTask
...
```

If you'd prefer to run all of these commands from a single terminal you can background the task with the following command:

```bash
$ ./script-worker &
```

If you'd like to turn off all of the output to the terminal, change the line

```go
const DEBUG = true
```

to:

```go
const DEBUG = false
```

before building the script-worker.
