Starting a Process from ELF executable file
===========================================
We all know that the standard file for representing executable, shared library and object file is ELF in UNIX based systems. 
In this post we will not talk about ELF file formats or any details of how to load it in to memory, 
but about the steps kernel does after loading ELF into memory and starting the process corresponding to it.

Assuming all process related entries are made in kernel data structures and memory is allocated for it, 
we start the steps on how kernel load, initialize and start executing a ELF executable file.

1. Kernel reads and load multiple sections of ELF files per the details in ELF header. Typically loading of sections are done lazily in a VM enabled Operating System (i.e. sections are loaded into memory based on need - whenever a page fault occurs).

2. Initialize the stack pointer by pointing to the top of the User segment (varies from architecture and OS). nothing but load the address of top of user segment into SP register.

3. Initialize the Instruction pointer by pointing to the start address taken from the ELF Header file.

4. Start the user process by simulating a return from an
 interrupt (typically some architecture specific assembly code)

That's it - when process returns to user mode - it start executing the code from the begin address from ELF header.
