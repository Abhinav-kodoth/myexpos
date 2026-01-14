# Documentation
This document summarizes key Operating Systems concepts learned through hands-on work with the eXpOS project at NIT Calicut.

follow complete [Roadmap](https://exposnitc.github.io/Roadmap.html)


## Step 1- 4

### Control Flow of BOOT ROM execution

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

## Step 5-8

### COMPLETE EXECUTION FLOW

```
1. POWER ON
      
   Machine starts, IP = 0
   Privileged mode

2.BOOT ROM EXECUTES (Page 0, addresses 0-511)
   LOADI(1, 0)  --- Load disk block 0 to page 1
   JMP 512      --- Jump to address 512

   (These stages are explained in Stage 3)
3. OS STARTUP CODE BEGINS (Page 1, address 512)

   a) LOAD COMPONENTS
       loadi(65, 7)      INIT to page 65
       loadi(66, 8)      INIT to page 66
       loadi(22, 35)     INT 10 to page 22
       loadi(23, 36)     INT 10 to page 23
       loadi(2, 15)      Exception to page 2
       loadi(3, 16)      Exception to page 3
   b. SETUP PAGE TABLE
      [PTBR+0]=65
      [PTBR+1]=0100

      Logical 0 and 1 is for code and 2 Represent Stack which needs valid Write bit
   c.INITIALIZE STACK
       [38912] = 0       Entry point at stack top
       SP = 1024         Stack pointer (logical)
   d. SWITCH TO USER MODE
       ireturn          ← Pop IP=0, switch mode

4.USER PROGRAM STARTS

   IP = 0 (logical)
   Translates to physical 33280 (page 65)

   Executes the user program
5.INT 10 EXECUTES (Back to privileged mode)
   
   Machine switches to privileged mode

   Machine Halts

