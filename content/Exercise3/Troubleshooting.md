---
title: "Troubleshooting"
date: 2022-04-26T19:29:27+02:00
draft: false
weight: 40
pre: "<b>D. </b>"
---

### Troubleshooting

If you're having trouble with the port "timing out", try reducing the port speed to 115200. If you're unable to reduce the port speed, you can open a terminal and run the following command:

```shell
$ esptool.py -p YOUR_PORT -b 115200 ...
```
and then copy/paste the failed command from the Arduino IDE window (the part after the `-p` section) into the terminal.

