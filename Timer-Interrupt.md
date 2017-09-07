How Timer Interrupt works?
==========================
Most of the system programmer used the Timer Interrupt for various reasons especially in synchronization. 
Some of the including me didn't spent much time on how exactly it works. 
This post is my attempt to explain my understanding on how it works?

Most of the IBM compatible PCs come with a hardware unit called **Programmable Interrupt Timer (PIT - Chip 8253 and 8254)** 
or an equivalent circuit embedded in Mother board. 
They have separate clock and **3 counter circuits** which can be programmed to track different tasks. 
- At the time of booting OS typically sets the frequency @ which it wants the timer interrupt. 
- This can be done by calling the appropriate assembly instruction to set the frequency. 
- Linux uses PIT to issue timer interrupts at about 100-Hz frequency (every 10 milliseconds).
- Once set, an external clock interrupt occurs @ specified frequency. 
- The interrupt vector will call corresponding interrupt handler, which in turn calls scheduler on given time frame => a swapping of processes.

## Useful resources:
http://en.wikipedia.org/wiki/Intel_8253
