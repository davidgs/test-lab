---
title: "Testing the Process"
date: 2022-04-26T20:01:44+02:00
draft: true
weight: 60
pre: "<b>F. </b>"
---

### Running the Process Without the Camera

From within the Web Modeler you can always start an instance of the process to test it. You will need to click the `Start Process` button on the top right of the modeler and add a JSON object containing some information to start the process:

```json
{"imageLoc": "https://davidgs.com:5050/pix/headshot.png", "isPicture": true }
```

That picture exists, and will be used to start an instance of the process to be evaluated.

