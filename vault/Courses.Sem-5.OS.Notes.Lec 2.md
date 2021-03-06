---
id: tFy23OlAvEHgWWoRF2db5
title: OS
desc: ''
updated: 1631170856980
created: 1630900277699
stub: true
---

# Evolution of OS and Kernel

## Evolution of OS
* Serial Processing
* Simple Batch Systems
* Multiprogrammed Batch Systems
* Time Sharing Systems
* many others

# Serial Processing
* There was no OS.
* To run the program, we would have to type a command for everything.
* A program at that time was called a job which is a set of instructions along with the data on which the instructions need to be executed.
* Issues
    * Scheduling
        * Fixed amount of time allocated to each instruction.
        * Conflict between instructions requiring more or less time.
    * Setup Time
        * Loading of compiler and program is time consuming

# Simple Batch System
* Monitor Program were used which were kind of OS - A very rudimentary OS.
* It is a software that controls the sequence of events.
* No direct access to users unlike Serial Processing.
* Job is submitted to an operator who batches similar instructions together and places them on the input device/hardware.
* In this way, the time consumed is averaged out and the processor can be utilized to its maximum.
* Control is given back to monitor after program gets terminated.
* Once submitted in batch sys, we cannot interact in between. Either it finishes or gives an error.

> Monitor is a special program that manages execution of each program in the **batch**. It controls the sequence of events. 
* Resident monitor (another name for simple monitor) is software always in memory. It reads in job and gives control to the processor which in turn returns the control back to monitor

* _"Control has passed to a job"_ : processor is fetching and executing instructions in a user program

* _"Control is returned to a monitor"_ : processor is fetching and executing instructions from monitor program

> Processor executes instructions from the memory i.e monitor which resides in the memory. It gains control from monitor to execute the task and once completed returns the control to monitor.

> JCL (Job control language) - It is a programming language that provides instruction to the monitor about the compiler and data to be used.

## Modes of operation
* User mode (Analogy: Normal Mode) - Programs submitted by the user to the memory and are executed in this mode. **Not all instructions may be executed. Errors are possible**
    * anything except OS operations
* Kernal mode (Analogy: Admin/root Mode) - Part of a modern OS that actually performs I/O Management, Process Management, Some things directly related to hardware etc. 
    * Kernal is the most important 
    * It is one which manages the above mentioned things which user mode cannot else we have high chance for it to get corrupted.
    
## Issues with simple batch system 
* Processor remains idle.
* Slow compared to processor even with automatic job sequence.

![](/assets/images/2021-09-09-12-07-07.png)

## Uniprogramming

> Processor must wait for I/O instruction to complete before proceeding further.

## Multiprogramming

> Opposite of uniprogramming. Still there will be some waiting time but at least it can be reduced and hence is better than uniprogramming.
* Reduces free time but tradeoff with memory

## Time sharing systems
* The program is being shared through different users and different monitors. Thus, can be used to handle multiple interactive jobs.
* Processor time is shared among multiple users.
* This time is in milli or micro seconds. This is called short burst or quantum computation.

![](/assets/images/2021-09-09-12-07-32.png)

## OS Structure
* *For general purpose OS, the program is very large.*
* Ways to structure OS
    * ### Monolitic Approach
        * (Analogy coding in C where there are no classes) - Everything combined in one place.
        * Eg. Older LINUX and UNIX
        * Advantages
            * Speed as everything is connected
            * Performance
        * Disadvantages
            * Difficult to maintain and modify
    * ### Layered Approach 
        * OS divided into number of layers.
        * Layer 0 (lowest layer) = hardware 
        * Layer n (highest layer) = user interface layer
        * A particular layer can use functions and services of **immediate lower-level layer only (layers below it).**
        * Eg. Older windows versions
    * ### Microkernels 
        * Move as much functionalities as possible to user mode from kernel mode. 
        * Little bit slow
        * Unlike that in layered and monolithic where majority of the functionalities is available in only kernal mode.
        * I\O and interrupt management, primitive memory management, inter-process communication and basic scheduling were kept in kernel mode.
        * All other functionalities will be running in user mode. They communicate internally by **message passing**
        * Advantages
            * Time is reduced significantly as the time to change the mode from user to kernel and vice versa is almost completely diminished.
            * Porting of OS to newer architecture becomes easier (will be covered in upcoming lectures).
            * More reliable because less code is running in kernel mode.
            * More secure as less code has to be valudated in kernel.
        * Disadvantages
            * Performance overhead to change the mode.
        * Eg. Mach, MINIX, Windows NT Client-Server
    * ### Modules 
        *  Most moedern OS implement kernel modules
        * These are loadable kernel module
        * Uses OOP
        * Similar to layers but is more flexible
        * Eg. Device Drivers (These are loaded as needed within the kernel)
        * Solaris Modular Approach (will be covered in upcoming lectures).
    * Solaris Modular approach
        * has seperate modules connected to kernal. So to add a functionality, u neednot compile whole kernel again.
    * Hybrid Approach - Combines multiple approaches to address performance, security and usability.
        * Eg. Linux and Solaris = monolithich + modular, windows = monolithic + microkernel and Mac OS and IOS = Darwin which is microkernel and BSD Unix kernel implemented over layered model