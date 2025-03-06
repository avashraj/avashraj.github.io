+++
date = '2025-03-05T17:27:55-08:00'
draft = false
title = 'Thread'
+++
from [Operating Systems]({{< relref "notes/CSE-150.md" >}})

A thread is the smallest unique unit of execution in a CPU. It is also the smallest piece of execution that can be 
scheduled independently by a scheduler in an operating system. A thread has its own
 - set of registers 
 - program counter
 - stack memory

Threads are a part of a larger process where they can share global variables, heap memory, and executable code with other
threads in the same process. A thread is executing when it is resident on a processor/core's registers. 


### **TCB**

Every thread has its own thread control block which is a data structure that holds important information about that thread.
A TCB contains
 - a unique ID 
 - the thread's PC or pointer to its next instruction
 - pointer to its stack
 - state of the thread eg. ready, waiting, running
 - the registers that would be in the CPU registers if it was running
 - its priority in terms of scheduling
 - a pointer to its associated process/PCB


We need a uniform data structure for threads for efficient context switching. 
