# Documentation
This document summarizes key Operating Systems concepts learned through hands-on work with the eXpOS project at NIT Calicut.

follow complete [Roadmap](https://exposnitc.github.io/Roadmap.html)


## Step 1- 4

```
Power ON
   ↓
CPU starts at IP = 0
   ↓
Boot ROM executes (page 0)
   ↓
Disk block 0 → memory page 1
   ↓
IP = 512
   ↓
Boot Block executes
   ↓
OS Startup Code runs
   ↓
Kernel initializes system

```
