---
layout: post
summary: "Choose the best File System for my cross-platform USB"
tags: tech
---
[TL;DR version](http://www.howtogeek.com/73178/what-file-system-should-i-use-for-my-usb-drive/):

- If you are sharing a drive between computers and don’t need to use big files, FAT32 works almost everywhere but doesn’t support files bigger than 4GB. This is the default for flash drives since it works everywhere.
- If you do need to use files bigger than 4GB, exFAT works on Windows, Linux (with FUSE), and OS X. This is probably the best choice for a shared hard drive that will only be plugged into a computer.
- If you are only adding files from Windows and you need to use big files, NTFS works almost everywhere, although is read-only on OS X and doesn’t work on some media players.

![https://i.imgur.com/rbxOCiu.png](https://i.imgur.com/rbxOCiu.png)

![https://i.imgur.com/VfCtNbE.png](https://i.imgur.com/VfCtNbE.png)
