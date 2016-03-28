---
layout: post
summary: "ACPI problem on legacy or old PCs"
tags: linux troubleshoot
---
Big news for today: my cousin's Win 7 got malfunctioned and he decided to try out Linux this time.

I got him a copy of ElementaryOS, but quickly disappointed at the boot screen, when the laptop kept raising ACPI problems.

Took me a while to find out a way to forcefully disable all ACPI and graphics settings: 

`all_generic_ide=1 pci=nommconf pci=noacpi ide=nodma acpi=off noapic nolapic noacpi nomodeset`

> http://ubuntuforums.org/showthread.php?t=2299362
