---
title: "Testing A Process Instance"
date: 2022-04-26T19:45:38+02:00
draft: false
weight: 30
pre: "<b>C. </b>"
---

### Testing the Process

From within the Web Modeler you can always start an instance of the process to test it. You will need to click the `Start Process` button on the top right of the modeler and add a JSON object containing some information to start the process:

```json
{"imageLoc": "https://davidgs.com:5050/pix/headshot.png", "isPicture": true }
```

That picture exists, and will be used to start an instance of the process to be evaluated.