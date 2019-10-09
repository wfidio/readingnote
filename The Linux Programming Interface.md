
## Two different meanings of operating systems

1. To denote the entire package consisting of the central software managing a computer's resources and all of the accompanying standard software tools, such as command line interpreters, graphical user interfaces, file utilities, and editors.

2. More narrowly, to refer to the central software that manages and allocates computer resources.

The term *kernel* stands for the second meaning.

## The main tasks that *kernel* performs:
- Process scheduling.
- Memory management.
- Provision of a file system.
- Creation and termination of process.
- Access to devices.
- Networking.
- Provision of a system call application programming interface.

## File I/O Model
- system call(open() , write(), close(), read()) used to perform I/O on all types of file.
- File descriptor. The I/O system call use file descriptor to open a file. It is a non-negative integer.
    - descriptor 0 is standard input.
    - descriptor 1 is standard output.
    - descriptor 2 is standard error.

## Programs 
- The first forms is source code.
- The second form is binary machine language instructions.

## Processes 
A process is an instance of an execution program. When the program is executed, the kernel loads the code of the program into the virtual memory, allocates space for program variables, and sets up kernel bookkeeping data structures to record various information.

- process memory layout
    - Text. the instructions of a program.
    - Data. the static variables used by the program.
    - Heap. an area from which programs can dynamically allocate extra memory.
    - Stack. a piece of memory that grows and shrinks as functions are called and return and that is used to allocate storage for local variables for function call linkage information.


- system call fork() can used to create a new child process that inherits data, stack, and heap segment from the parent process. 

- Process ID and parent process ID.
    - each process has a unique identifier call PID and the parent process identifier called PPID
- Process termination
    - process can be terminated in two ways. One is requesting its own termination by the system call exit(), or being killed by delivery of a signal.
    - process can yield a termination status, a small nonnegative integer that is available for inspection by the parent process by the system call wait()

- init process
    when booting the system, the kernel creates a special process called init. All processes on the system are created either by init or by one of its descendants.
    - the init process has the PID 1 and runs with supervisor privileges.
    - the main task of init is to create and monitor a range of processes required by a running system.

- daemon processes
    A daemon process is a special-purpose process that is created and handled by the system as other process but has several distinctive characteristics:
    - It is long-lived. This kind of process is often started at system booting and remains until the shut down of the system.
    - It runs in the background, and has no controlling terminal from which it can read input or to which it can write output.

- Resource limits
    Each process consumes resources, such as open files, memory, and CPU time. And almost all of the limits can be separated into 2 different kinds.
    - Soft limit, which limits the amount of the resource that the process may consume.
    - Hard limit, which is a celling on the value to which the soft limit may be adjusted.

## static and shared library

A object library is a file containing the compiled object code for a set of function that may be called from application programs. Modern UNIX systems provides two types of object libraries.
- static libraries
- shared libraries 


## Interprocess Communication and Synchronization

One way for process to communicate is by reading and writing information in disk files.However, for many applications, this is too slow and inflexible.

To resolve the IPC(Interprocess Communication) problem, the modern UNIX system provides a rich set of mechanism.
 - signals.
    It is used to indicate that an event is occurred.
 - pipes.
    It is used to transfer data between processes.
 - sockets.
    It can transfer data from one process to another process, either on the same host computer or on different hosts connected by a network.
 - file locking.
    It allows a process to lock regions of a file in order to prevent other processes from reading or updating the file content.
 - message queues.
    Exchanging messages(a packet of data) between process.
- semaphores.
    It is used to synchronize the action of processes.
 - shared memory.
    It allows two or more processes to share a piece of memory, when one process change the contents of shared memory, all of the other processes can immediately see the changes.


## Signal 
Signals have a wide range of implementations of other context more than the IPC.
Signals are often described as "software interrupts", the arrival of signals informs that some events or exceptional conditions has occurred.
The signal has several types and has the symbolic name of the form SIGxxxx.
The signals are sent to a process by kernel, or by other kernels, or by the process itself.
The situations that the kernel will send a signal to a process.
- the user typed the interrupt character.
- one of the process's child process has been terminated.
- a timer set by the process has expired.
- the process attempted to access an invalid memory address.

And when the process receive a signal, it will take some actions like:
- ignores the signal.
- killed by the signal.
- suspended until later being resumed by receipt of a special-purpose signal.

## Thread
In modern UNIX implementation, each process can have multiple threads of execution. 
Thread can be imaged as a set of processes that shared the same virtual memory. Each thread is executing the same program code and same data area and heap. However, the each thread has its own stack containing the local variables and function call linkage information.
Thread can communicate with each other via the global variables that they are sharing(Like the condition variables and mutexes provided by the threading API).
Advantages of using threads:
- making it easy to share data(via the global variables) between cooperating threads.
- some algorithms transpose more naturally to a multithreaded application than to a multiprocess implementation. 

## Pseudoterminals 
A pseudoterminal is a pair of connected virtual devices, known as the *master* and *slave*.
The key point about a pseudoterminals is that the slave device provides an interface that behaves like a terminal, which makes it possible to connect a terminal-orientated program to the slave device and then use another program connected to the master device to drive the terminal-orientated program.
(like telnet or ssh)


## Client-Server Architecture
A client-server application is one that is broken into two component processes.

- *client*. Client asks the server to carry out some service by sending it a request message.
- *server*. Server examines the client's request, performs appropriate actions, and send response message back to the client.

Servers may implement a variety of services:
- providing access to a database or other shared information resource.
- providing access to a remote file across a network.
- encapsulating some business logic.
- providing access to a shared hardware resource.
- serving web pages.

Encapsulating a service within single server is useful for a number of reasons.
- Efficiency. Cheaper to provide one instance of a resource that is managed by a single server than to provide the same resource locally on every computer.
- Control, coordinate, and security.
- Operation in a heterogeneous environment. In a network, the various clients, and the server, can be running on the different hardware and operating system platform.

## The /proc File System
The /proc file system is a virtual file system that provides an interface to kernel data structures in a form that looks like files and directories on a file system.
This provides an easy mechanism for viewing and changing various system attributes.
(/proc/PID)

## System Calls
A system call is a controlled entry point into the kernel, allowing a process to request that the kernel performs some actions on the process's behalf.

General points of the detail of how system call works
- System call changes the processor state from user mode to kernel mode, so that the CPU can access protected kernel memory.
- Each system call is identified by a unique number.
- Each system call may have a set of arguments that specify information to be transferred from user space.

## Library Functions

A library function is simply one of the multitude of functions that constitutes the standard library.

Many library functions do not make any use of system calls while some library functions are layered on top of system calls.

## Atomicity and Race Conditions

Atomicity is a concept that we'll encounter repeatedly when discussing the operation of system calls. All system calls are executed atomicity. By this, we mean that the kernel guarantees that all of the steps in a system call are completed as a single operation without being interrupted by another process or thread.

Atomicity allows us to avoid race conditions(sometime known as race hazards). A race condition is a situation where the result produced by two processes operating on shared resources depends in an unexpected way on the relative order in which the processes gain access to the CPUs.

