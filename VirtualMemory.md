Virtual Memory
==============
VM is typically implemented with both Hardware unit and Operating System software unit.
I see 2 main advantages in VM
- It allows users to use more memory for a program than the real memory of program.
- In a multi-programming environment, different programs run in isolation and secured access to only its memory is guaranteed by VM

## How VM works?
If your computer **runs out of physical memory**, it writes some of the unused data to some temp location in disk (called as swap space) and frees that memory. 
When the swapped part is requested again, they are brought back to main memory again from disk (swap space). 
Another important aspect is to do with **multiprogramming**. 
When process context switch happens, we need to ensure proper usage of memory so that there are no security compromises. 
To achieve this the physical memory and disk are splitted into small units of addressable memory called as pages. 
Pages of data are brought in and out physical memory and every process has its own mapping of the allocated physical page to ensure righteous usage. 
This mapping is typically called as Page Table.

## Virtual Address and Physical Address:
All the addresses used by programmer (which we see in program) are virtual address and all these addresses together form the address space for the program.
An addressable unit in physical memory is called physical address. The page table usually has the mapping of virtual to physical addresses. 

## Page Replacement Algorithms:
The logic of which page to be evicted, when there is a need of physical memmory page is called Page Replacement Algorithm. 
There are various algorithms used by OS (LRU, FIFO, OPT). we can discuss them in some other posts.
