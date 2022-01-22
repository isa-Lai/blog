---
layout: post
title: Process in Operating System
date: 2021-09-12 14:13:55
categories: [CS,Operating System]
tags: [Operating System]
toc: true
---

In all operating system, **Process**(进程) and **Thread**(线程) are important concept. Process is an execution of a program.

<!-- more -->
## Process
A process is the execution of a program that allows you to perform the appropriate actions specified in a program.
CPU (single core) swich quickly between different processes to perform (fake) parallel computing.
- A program by itself is not a process
- A process is an active entity
- Is is possible that two processes could be associated with the same program

### Process in Memory
1. Test section - executable code
2. Data - global variables
3. Heap = memory tht is dynamically allocated during program run time
4. Stack - Temporary dats storage when invoking functions

### Execution and Trace
- Process is used to excute machine instrctions residing in main memory
- From the processor point of view, it execute instru from its collection of instruc in some sequence indecated by the changing values in the register known as the **Program counter PC** or **Instruction pointer**
- Behavior of an individual process can be characterized by listing the sequence of instruction that execute for that process. Such listing is **Trace** of process (跟踪)
- Can be characterized by showing the way in which the trace of various processes are interleaved
  
### Stage Process Model
#### Two State
- Running
- Not-Running
  - Processes in this stage is kept in **Queue**, waiting to run in a list

![Two State Transition](https://slaystudy.com/wp-content/uploads/2020/07/2state.png)

#### Five State
- Blocked - cannot execute until some event occurs
  - Their may be more than 1 Block Queue for arrange many process
![Five State Transition](https://miro.medium.com/max/821/1*dhW-U0e6VFV7ML6UkiuEYQ.png)

#### Seven State
- See more detial in Suspend Process section below
![Seven State Transition](https://www.researchgate.net/profile/Mohsen-Sharifi-6/publication/268347340/figure/fig9/AS:668228732870656@1536329553126/Seven-state-transition-diagram-The-NEW-TERMINATED-READY-RUNNING-and-BLOCKED-states.jpg)

### Process Control Block
**PCB** or **tack control block** with info of:
- Process State
  - New
  - Ready
  - Running
  - Halt
  - ...
- Program Counter - address of next statement 
- CPU Register - several register like accumulators, index, stack pointer ......
- CPU-Scheduling Info
  - Process priority
  - pointer to scheduling queues
  - other scheduling parameter
- Memory-Management Info
  - value of base and limit register
  - pages tables
  - segmentation table
- Accounting info
  - Amount of CPUand real time used
  - time limits
  - process number
  - ...
- I/O Status Info - list of I/O devices allocated to the process, a list of open list and ...

### Process Module
#### Sequential Process
- A process is an execution of an instance, eg register, counter.
- Every core in cpu execute one process at the time
- Process is an action, it have programm, input, output, and status.
- If a program runs twice, it is two processes.

### Suspended Process
#### Definition
- problem that process need to wait I/O
- Solution
  - Expand main memory
  - **Swapping** - move some process form main memory to the disk using suspend

![Seven State Transition](https://www.researchgate.net/profile/Mohsen-Sharifi-6/publication/268347340/figure/fig9/AS:668228732870656@1536329553126/Seven-state-transition-diagram-The-NEW-TERMINATED-READY-RUNNING-and-BLOCKED-states.jpg)

- Ready: in main memory & available for execution
- Blocked: in main memory & awaiting an event
- Blocked, Suspend: In secondary memory & awaiting an event
- Ready, Suspend: in secondary memory & available to execution as soom as it is loaded into main memory


#### Cause
- Swapping
- Interactive user request
- Timing - for periodically executed
- Parent process request
- Other OS reason - like if the process can cause problem

### Creation of Process
Events that lead to process creation are
- System initialization
- Interactive Log On
- User request to create a new process
- Batch job initialization - create in response to the submission of a job
- Execution of a process creation system call by a running process (Spawned by existing process)
  - Parent and chiled process


Step:
- Build data structure that used to manage the process
- Allocates the address space to used by the process


Some back-end process, like email, web page, are call **Daemon**(守护进程). This type of process sleep when it is not used. 

In **Windows**, user can open different window, each window represent one process. It can also use `CreateProcess`.

In **UNIX**, using `fork` to create new process.  
1. `fork` create a copy of the executing process.
2. Child process use `execve` or other to switch to another process.
Process creation using fork():
![Process Diagram](https://www.tutorialspoint.com/assets/questions/media/12684/Process%20Creation%20using%20fork().PNG)

### Termination of Process
Causes of process termination are:
- Normal Ternimation - Execution is naturally completed. Process leavs the processor and releases all its resources.
- Parentm Request - Parent process requests for termination on child
- Parent Termination - Parent end, child end
- Memory Unavailable
- Bounds Violation - access to memory that is not allowed
- Time Limit Exceeded - run longer than a total time
- Time Overrun - run longer n a certain event
- Protection Error - using resource or file that is not allowed
- Atithmetric Error - process try a prohibited computation like 1/0
- Failure occurs (like I/O)
- Invalid Instrction
- Orivilegde Instruction - attempts to use an ins reserved for the OS
- Data Misuse - wrong type data
- OS or Operator Intervention - kill process

Termination in
- UNIX: `exit`
- Win: `ExitProcess`

### Process Hierarchies
进程层次结构
- Parent can create multi child process, while child process can have only one parent process.
- In UNIX, process process like tree hierarchy. The root is `init` process. This structure cannot change
- In Win, all processes have the same priority. Parent process will have a **handle**句柄 to controll the child.  It can pass the handle to other process.

### Process State
![Process States](https://i0.wp.com/www.cplusplus.in/wp-content/uploads/2020/09/1254.png?w=856&ssl=1)

Note to some states:
- Ready 就绪: Many processes may be present in ready.  Can execute but not because other process is executing
- Run 运行: Assigned the CPU for execution
- Blocked or wait 阻塞: Run will moving to this state if it need I/O operation or some blocked resource during its execution. After that, move to ready.

### Implementation of Process
The operating system maintain a **process table**进程表 
- A process an entry in the table
- Table tell the info about the states of the processes, eg
  - program counter
  - stack pointers
  - allocated memories
  - status of the files
  - accounting and scheduling info

Sample Table Field:
<table class=cms-table><tbody><tr><td><strong>Process Management</strong><td><strong>Memory Management</strong><td><strong>File Management</strong><tr><td>Registers<td>Pointer to text segment info<td>Root directory<tr><td>Program counter<td>Pointer to the data segment info<td>Working directory<tr><td>Program status word<td>Pointer to stack segment info<td>File descriptors<tr><td>Stack pointer<td><td>User ID<tr><td>Process state<td><td>Group ID<tr><td>Priority<td><td><tr><td>Scheduling parameters<td><td><tr><td>Process identity<td><td><tr><td>Parent process<td><td><tr><td>Process group<td><td><tr><td>Signals<td><td><tr><td>Time when process started<td><td><tr><td>CPU time used<td><td><tr><td>CPU time of children<td><td><tr><td>Time of next alarm<td><td></table>

Sample lowest level of execution when interrupt occurs
1. Hardware stacks program counter, etc.
2. Hardware loads new program counter from interrupt vector.
3. Assembly language procedure saves registers.
4. Assembly language procedure sets up new stack.
5. C interrupt service runs (typically reads and butters input).
6. Scheduler decides which process is to run next.
7. C procedure returns to the assembly code.
8. Assembly language procedure starts up new current process.

### Modelling Multiprogramming
`CPU usage = 1-p^n`
- p: (time of waiting I/O)/(time it stays in memory)
- n: **Degree of multy programming** is the number of processes
![Multiprogramming Model](https://tse1-mm.cn.bing.net/th/id/R-C.ca5cc6152cfcfe65cd2e0da28d3ced70?rik=6Kj%2byfFUKuj98A&riu=http%3a%2f%2fboron.physics.metu.edu.tr%2fozdogan%2fOperatingSystems%2fweek4%2fimg15.png&ehk=Pf%2fGJVvnwPoxFmiSlApkWe68SvBQo7a31lGJGb8V1AY%3d&risl=&pid=ImgRaw&r=0)

Example:
If processes have 80% I/O wait, it need 10 processes in memory to reduce CPU waste within 10%.




 
