## Unix Philosophy

Few characteristics shared by typical UNIX programs and systems.
- Simplicity. Many of the most UNIX utilities are very simple and, as a result, small and easy to understand
- Focus. It is often better to make a program one task well than to throw in every feature along with the kitchen sink.
- Reusable Components.
- Filters.
- Open File Formats.
- Flexibility. 

## Linux Programs

Linux applications are represented by two special types or files: *executables* and *scripts*.

Executable files are programs that can be run directly by the computer.
Scripts are collections of instructions for another program, and interpreter.

## The C programs 
On POSIX-compliant system. the C compiler is called c89. The C compiler is simply called cc.

## Development System Roadmap

#### Applications

Applications supplied by the system for general use, including program development, are found in /usr/bin.

Applications added by system administrators for a specific host computer or local network are often found in /usr/local/bin or /opt

#### Header Files
For programming in C and other languages, you need header files to provide definitions of constants and declarations for system and library function calls.

For C, these are almost always located in /usr/include

#### Library Files
Libraries are collections of precompiled functions that have been written to reusable. 

Standard system libraries are usually stored in /lib or /usr/lib.

A library filename always start with lib.Then follows the part indicating what the library is. The last part of the name starts with a dot and specifies the type of the library.

- .a for the traditional, static libraries.
- .so for the shared libraries.


#### Static Libraries
The simplest form of library is just a collection of object files kept together in a ready-to-use form.
The complier and linker take care of combining the program code and the library into a single execution program.

Static libraries, also known as archives, conventionally have names that end with .a. 

One disadvantage of static libraries is that when you run many applications at the same time and they all use functions from the same libraries, you may end up with many copies of the same functions in memory and indeed many copies in the program files themselves.


#### Shared Libraries 

Shared libraries are shared in the same places as static libraries, but shared libraries have a different filename suffix, .so

when a program uses a shared library, it is linked in such a way that it does not contain the function code itself, but references to shared code that will be made available at the run time.

An additional benefit of the shared library is that the shared library can be updated independently of the applications that rely on it.


#### Why program with a Shell?

One reason to use the shell for programming is that you can program the shell quickly and simply. Moreover, a shell is always available even with most basic Linux installation.

#### What is a Shell?

A Shell is a program that acts as an interface between you and the Linux system, enabling you to enter commands for the operation system to execute.

#### Environment Variables 

\$HOME : The home directory for the current user
\$PATH : The directory for the search of the command
\$PS1 : A command prompt, frequently $
\$PS2 : A secondary prompt, usually  >
\$IFS : An input field separator.
\$0 : The name of the shell script.
\$# : The number of parameters passed.
\$\$ : The process ID of the shell script.

#### Parameter Variables
\$1,\$2, ... : The parameters given to the shell scripts.
\$* : A list of all the parameters., in a single variable, separated by the first character in the environment variable IFS.
\$@ : A subtle variation on \$*. It does not use the IFS environment variables.

#### Conditions
Fundamental to all programming languages is the ability to test conditions and perform different actions based on those decisions.

- the test or [ Command
In practice, most scripts make extensive use of the [ or test command, the shell's Boolean Check.

- the : command
The colon command is a null command. It's occasionally useful to simplify the logic of condition., being an alias for true.Since it's built in. : run faster than true

- the . command
The dot(.) command executes the command in the current shell
when a script executes an external command or script, a new environment(a subshell) is created, the command is executed in a new environment, and the environment is then discarded apart from the exit code that is returned to the parent shell.


#### Commands

- echo 
output a string with a newline character.

- eval
this command enables you to evaluate arguments.

- exec
exec command has two different uses. Its typical use is to replace the current shell with a different program. No lines in the script after the exec will be processed.
the second use of exec is to modify the current descriptors.

- exit n
The exit command causes the script to exit with exit code n.
In shell script programming, exit code 0 is success, and codes 1 through 125, inclusive, are error codes that can be used by scripts.
code 126: the file is not executable.
code 127: a command was not found.
code 128 and above: a signal occurred.

- expr 
The expr command evaluates its arguments as an expression.

- shift 
The shift command moves all the parameter variables down by one, so that \$2 becomes \$1

- trap
The trap command is used to specify the actions to take on receipt of signals.  A common is to tidy up a script when it is interrupted.


#### Linux File Structure
files in Linux environment are particularly important, because they provide a simple and consistent interface to the operating system services and devices. In Linux, *everything is file*

This means that, in general, programs can use disk files, serial ports, printers, and other devices in exactly they use files.

Directories are special sort of files.

#### Directories

The properties of a file are stored in the file's inode, a special block of data in the file system that contains the length of the file and where on the disk it is stored.

A directory is a file that holds the inode numbers and names of other files.Each directory entry is a link to a file's inode.

#### Files and Devices
hardware devices are very often represented(mapped) by files.

Three important devices found in both UNIX and Linux

- /dev/console
The device represents the system console.Error messages and diagnostics are often sent to this device.

- /dev/tty
The special file /dev/tty is an alias(logical device) for the controlling terminal(keyboard and screen, or window) of a process, if it has one.

- /dev/null
The /dev/null file is the null device. All output written to this device is discarded. An immediate end of file is returned when the device is read, and it can be used as a source of empty files by using the cp command.

#### System Calls and Device Drivers

low-level function used to access the device driver, the system call, include:
- open: open a file or device
- read: Read from an open file or device
- write: Write to a file or device
- close: Close the file or device
- ioctl: Pass control information to a device driver

One problem with using low-level system calls for input and output is that they can be very inefficient. And the reason:
- There is a performance penalty in making a system call. System calls are therefore expensive compared to function calls because Linux has to switch from running your program code to executing its own kernel code and back again.
- The hardware has limitations that can impose restrictions on the size of data blocks that can be read or written by the low-level system call at any one time.

To provide a higher-level interface to devices and disk files, a Linux distribution provides a number of standard libraries.

#### Write
The write system call arranges for the first *nbytes* from *buf* to be written to the file associated with the file descriptor *fildes*. It returns the number of bytes actually written.

#### Read
The *read* system call reads up to *nbytes* bytes of data from the file associated with the file descriptor *fides* and places them in the data area *buf*. It returns the number of data bytes actually read.

#### Open
In simple terms, *open* establishes an access path to a file or device. If successful, it returns a file descriptor that can be used in *read*, *write*, or other system calls.

#### umask

The umask is a system variable that encodes a mask for file permissions to be used when a file is crated. 
The value is a three-digit octal value. Each digit is the result of ORing values from 1,2 or 4;

#### close
close is used to terminate the association between a file descriptor and its file descriptor. After that The file descriptor becomes reusable.


#### ioctl
ioctl is a bit a ragbag of things. It provides an interface for controlling the behavior of device and their descriptors and configuring underlying services.

#### The Standard I/O Library
The standard I/O library and its header file, stdio.h, provide a versatile interface to low level I/O system call.

#### The /proc File System
Linux provides a special file system, *procfs*, that is usually made available as the directory /proc. It contains many special files that allow higher-level access to driver and kernel information.

#### Canonical versus Non-Canonical Modes

By default, terminal input is not made available to a program until the user presses Enter or Return.
This behavior is called canonical, or standard mode. All the input is processed in terms of lines. Until a line of input is complete.
The opposite of this is the non-canonical mode,where the application has much greater control over the processing of the input characters.


#### The termios Structure 
*termios* is the standard interface specified by POSIX and is similar to the System V interface termio
The terminal interface is controlled by setting values in a structure of type termios and using a small set of function calls.

The values that can be manipulated to affect the terminal are grouped into various modes.
- Input
- Output
- Control
- Local
- Special control character

#### Input Modes
The inputs modes control how input(character received by the terminal driver at a serial port or keyboard) is processed before being passed on to a program.

#### Output Modes
These modes control how output characters are passed; that is, how characters sent from a program are processed before being transmitted to the serial port or screen.

#### Control Modes
These modes control the hardware characteristics of the terminal.

#### Local Modes
These modes control various characteristics of the terminal.

#### Special Control Characters
Special Control Characters are a collection of characters, like Ctrl+C, acted upon in particular ways when the user types them.

#### Virtual Console
Linux provides a feature called virtual consoles. A number of terminal devices are available, all of which share the PC's screen, keyboard, and mouse. The virtual consoles are made available through the character devices /dev/ttyN where N is number, starting at 1.

#### Compiling with curses
The *curses* library takes its name from its ability to optimize the movement of the cursor and minimize the updates needed on a screen, and hence, reduce the number of characters that need to be sent to a text-based terminal.

#### Data Management 
3 ways of managing data in Unix:
- Dynamic memory management.
- File locking.
- the dbm database.

#### File Locking
File locking is very important part of multiuser,multitasking OS. Programs frequently need to share data, usually through files, and its very important that those programs has some way of establishing control of file.

Linux has several features that you can use for file locking. The simplest way is to create lock files in an atomic way.
The second method is more advanced. It enables programs to lock parts of a file for exclusive access.

#### Locking Regions

Creating lock files is fine for controlling exclusive access to resources such as serial ports or infrequently accessed files, but it is not suitable for the large shared file.

#### Deadlocks

Deadlock is always mentioned in the discussion of the locking.

Suppose two programs wish to update the same file, they both need to update the same file. They both need to update the byte 1 and byte 2 at the same time. Program A choose to update the byte 2 first then byte 1 and Program B choose to update the byte 1 first then byte 2.

Both programs start at the same time. Program A locks byte 2 and Program B locks byte 1. Program A tries for a lock on byte 1, since it is locked by the program B, program A wait. And the same as Program B.

The situation when neither program is able to proceed, is called deadlock, or deadly embrace. It is a common problem with database applications in which many users are frequently trying to access the same data.

#### Databases
Why using the database

- the data records can be stored vary in size, which is difficult to implement using flat, unstructured file.
- Databases store and retrieve data efficiently using an index. The big advantage is that this index need not to be a simple record number, which would be quite easy to implement in a flat file, but can be an arbitrary string.

#### The dbm Databases

All version of Linux, and most flavors of UNIX, comes with a basic, but very efficient, data storage set of routines called the dbm database. The dbm database is excellent for storing indexed data that is relatively static.

*introduction to dbm*
    
In spite of the rise of free relational databases, the dbm database continues to play an important role in Linux. Distributions that use RPM, such as Red Hat and SUSE, use dbm as the underlying storage for installed package information. The open-source implementation of LDAP, OPENLADP, can also use dbm as a storage mechanism.
    
    
The advantages of dbm is that it is very lightweight, and much easier to build into a distributed binary because no separate database server installation is required. 

