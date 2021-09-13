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

### Process Module
#### Sequential Process
- A process is an execution of an instance, eg register, counter.
- Every core in cpu execute one process at the time
- Process is an action, it have programm, input, output, and status.
- If a program runs twice, it is two processes.

### Creation of Process
Events that lead to process creation are
- System initialization
- Execution of a process creation system call by a running process
- User request to create a new process
- Batch job initialization


Some back-end process, like email, web page, are call **Daemon**(守护进程). This type of process sleep when it is not used. 

In **Windows**, user can open different window, each window represent one process. It can also use `CreateProcess`.

In **UNIX**, using `fork` to create new process.  
1. `fork` create a copy of the executing process.
2. Child process use `execve` or other to switch to another process.
Process creation using fork():
![Process Diagram](https://www.tutorialspoint.com/assets/questions/media/12684/Process%20Creation%20using%20fork().PNG)

### Termination of Process
Causes of process termination are:
- Execution is naturally completed. Process leavs the processor and releases all its resources.
- Parent process requests for termination on child
- Process tries to use a resource that it is not allowed
- Failure occurs (like I/O)
- Kill by other process

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


 
