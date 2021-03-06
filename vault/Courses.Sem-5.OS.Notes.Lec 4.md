---
id: tFy23OlAvEHgWWoRF2db5
title: OS
desc: ''
updated: 1631341847442
created: 1630900277699
stub: true
---



# Process: Description and Control

4 imp functions of os
* File management
* Memory management
* Process management - Fundamental task
* IO management 

## Requirements of OS as a Process Manager
* Interleave the execution of multiple processes. Here we assume that there is always a single processor system.
* Allocate resources to processes and protect them from each other especially in the case where both processes are using same files, to avoid any clashes.
* Enable process to share and exchange information. Eg. Parent and Child processes.
* Enable synchronization among processes.

## What is a Process?
* Program in execution.
* Instance of program running
* Entity that can be assigned to and executed on a processor
* **Unit of activity characterized by the execution of a sequence of instructions, a current state and an associated set of resources**
* Process Elements
    * Program code (generally shared)
    * Set of data
    * Attributes that describes the state
    
## Attributes - maintained in PCB
* Indentifier - Unique ID of each process
* State - Current situation of the process (Either running or not running)
* Priority - Self explanatory
* Program Counter - Keeps information about next process to be executed
* Memory pointers - Pointers to program code and data to be processed. Along with this, it also includes shared memory blocks.
* Context data
* I/O status information - Eg. List of files in use by the process etc.
* Accounting information - Eg. Time limits, clocks used etc.

> _In short the attributes can be called as meta-data_ (things apart from the program and data, these are the things which manage and drive the process).

## Process Control Block (PCB)
* All the attributes discussed above are maintained in this block.
* Basically, it is a type of data structure.

> **Thus, process is a combination of program code, associated data and PCB**

## Running on single resource
* To manage multiple processes on a single resources then scheduling comes to the picture.
* Thus, you allocate certain span of time to each process and once it gets finished, immediately another process starts.
* It gives an appearance that every process runs at the same time because the total time taken by all the process combined is really small.
* **Trace - List of instructions that are executed by a process.**
* **Dispatcher - Program that switches the processor from one process to another.** It is a type of short term scheduler.

## Execution of Processes by Processor
* Suppose that there are some processes which have a lot of instructions to execute. This might take time which is greater than the allocated one.
* So in the middle of the execution of a process, dispatcher stops the execution and decides which process should go next.
* Once decided, either execution of new process starts or execution of old process continues.
* Then, suppose there is an I/O request. Since this is a slow operation, the dispatcher will allow another process to run on the processor.
* This goes on and on untill all the processes are executed.

> The above method is from **processor POV** and is called **interleaving of processes** and the OS manages this through **dispatcher**. From **process POV**, the process gets executed sequencially.

## Process States
* Two states
    * Running
    * Not running
* Transition from **not running** to **running** state is called **dispatch** and is called **pause** for the opposite scenario.
* There can be at most only one process in running state at a given instance of time.
* There are 'n' number of processes in the non-running state.
* Thus, to manage all these processes, we need **queue** as the data structure.

## Note
* The below picture lists conditions under which a process can be created or terminated.
![](/assets/images/2021-09-10-23-18-55.png)
* Process spawning means event where a process creates a new process.

## 5-State Process Model
* Conditions when the process which is running will pause and enter in the queue:
    * Time slot alloted to the process is over.
    * Made some I/O request which may take time.
* Now, dispatcher needs to identify which processes are ready to be executed and then_ dispatch it from the middle of the queue._ This process is **time consuming and complex.**
* **Solution:**  OS must maintain multiple queues. Since there are two types of processes
    * Waiting - one who did not terminate but their allocated time got over and others who are waiting for I/O or other resouces.
    * Others that are ready to be dispatched and timeout ones (alloted time is over).
*  _**This, in turn is the 5-state process model.**_
* Total states in this model
    1. New - Process that has just been created but not admitted to the pool of the ready state processes.
        * **Not loaded in main memory but is created.**
        * This means that PCB for that process has been created but its corresponding data and program has not been loaded/created in the main memory.
    2. Ready - DS: queue
    3. Blocked/Waiting - DS: queue
    4. Running 
    5. Exit (Earlier it was not a state but now it is) - Process which has been released from the pool of processes.
        * However, there is some part of PCB left in main memory for accounting.

![](/assets/images/2021-09-11-11-43-14.png)

## State Transitions

![](/assets/images/2021-09-11-11-51-30.png)

* Ready and Blocked process can enter directly to exit state when its parent process has terminated or the process is terminated by the OS.
* When process spawning occurs, then child process is created in the new state.
* Hang state is equivalent to blocked/waiting state. If we remove it, it is directly moved to exit from ready state.
![](/assets/images/2021-09-11-11-54-33.png)
* **Problems** - 
    * Suppose there are 10 processes which are in blocked queue waiting for HDD to get accesible and there are 90 processes that are in hang mode.
    * Now once HDD is ready to be accessed, OS will have to search this blocked queue and move all these processes to ready state.
    * This is again time consuming and complex. Hence **multiple blocked queue model emerged**.


## Multiple Blocked Queue
![](/assets/images/2021-09-11-11-57-07.png)
