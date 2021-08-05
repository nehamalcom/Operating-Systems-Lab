# exPOS (Experimental Operating System)

- Initialised data structures in XSM include the disk free list, inode table, user table and root file.
- Disk free list tracks used and unused disk blocks.
- Inode Table contains information such as the file type, file name, file size, userid, permission and the block numbers of the data blocks of the file.
- The OS Startup code at block 0 is run when machine is started using bootstrap loader.
    i. The privilege mode is changed from KERNEL to USER mode
    ii. The instruction pointer is set to the value at the top of the user stack
    iii. The value of SP is decremented by 1
- The virtual address space of a user mode program is a contiguous address space starting from 0 to 512*PTLR-1
- Running machine in unprivileged mode:
    - When a program runs in unprivileged mode on the XSM machine, only a restricted machine model is available to the application program
    - Paging allows the OS to provide each application program running in unprivileged mode with a virtual (or logical) address space
    - The application's access can be restricted to this address space
    - The OS maintains a seperate page table for each program that maps the logical pages of each program to the corresponding physical pages
    - While executing in user mode, if an instruction in the application refers to a logical address beyond this limit, the machine will raise an exception
- Software Interrupts (traps) are the mechanisms by which user mode programs can transfer control to the code that runs in the kernel mode
- OS handlers that can be called from application programs for privileged tasks are known as system call routines
- To isolate the kernel from the user stack, the OS kernel must maintain two stacks for a program - a user stack and a kernel stack
- eXpOS maintains a Process Table, where data such as value of the kernel stack pointer, user stack pointer etc. pertaining to each process is stored
- The kernel maintains a data structure called System Status Table where the PID of the currently executing user process is maintained
- Idle is a user program which is loaded for execution during OS bootstrap
- Boot module is designed for the purpose of OS startup
- We employ round-robin scheduling in expOS
- The resource manager module manages resources like terminal, disk, inode etc. among different processes
- The disk interrupt handler makes use of the loadi instruction which abstracts disk I/O using the method of polling and the load instruction which abstracts interrupt based disk I/O
- We implement demand paging (lazy allocation) which allows more concurrent processes to run
- OS include semaphores which are primitives that allow concurrent processes to handle the critical section problem
- Binary semaphores can be used by user programs to synchronize the access to the shared resources so that data inconsistency will not occur

All functioning codes of various stages to in creating eXpOS using the roadmap: http://exposnitc.github.io/Roadmap.html
