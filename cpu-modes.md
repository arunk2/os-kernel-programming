Kernel mode & User mode
========================

As we all know that CPU (micro-processor) executes all the instructions.

Most of the modern architectures support at least 2 modes of CPU operation. Even if architecture supports more than 2 modes, they are usually grouped under 2 modes to have compatibility (of OS - across all machines).

* Mode 1 - Every operation possible is allowed
* Mode 2 - Some operations are restricted 

> **Restricted operations:** Instruction involving Hardware and RAM. If invoked in mode 1, the current execution/context is killed => violating process will be terminated


|Mode | Other names|
|-----|------------|
|Mode 1 | Kernel mode, Unrestricted, Supervisor, Ring 0|
|Mode 2 | User mode, Restricted, Unsupervised, Ring 3|

Most trusted codes is allowed to run in Mode 1. Usually kernel code of operating system executes in this mode.
All other codes execute in user mode.


***Following source are really good***
* http://www.codinghorror.com/blog/2008/01/understanding-user-and-kernel-mode.html
* http://en.wikipedia.org/wiki/CPU_modes
* http://stackoverflow.com/questions/1311402/differences-between-user-and-kernel-modes
