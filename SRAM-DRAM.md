SRAM and DRAM
=============
Everyone of us are familiar with RAM (Random Access Memory), this post is an attempt to explore the different types of RAM and how they store the data.

We typically have 2 types of RAM
- SRAM (Static RAM)
- DRAM (Dynamic RAM)

### How they get their name?
- DRAM requires the data to be refreshed periodically in order to retain the data.
- SRAM does not need to be refreshed as the transistors inside would continue to hold the data as long as the power supply is not cut off.

### How they are implemented?
- DRAM is implemented with a transistor and a capacitor for storing a bit of data.
- SRAM requires little complicated circuit with 6 transistors for storing a bit of data.

### Why DRAMs are Cheap compared to SRAM?
From the above details SRAM is little complex entity compared to DRAM. 
i.e. a DRAM can have almost 6 times more capacity with a similar transistor count to an SRAM. 
Hence, SRAM are costlier than DRAM.

### Power consumption:
For proper functioning of the DRAM, the capacitors in DRAM needs to be refreshed every 64 ms or less 
(typically they are given by manufacturers and managed by DRAM controller). 
Hence, DRAM consumes more power. 
Typically in Battery based powered devices, they consume huge portion of power. 
Research has been going around to optimize this refreshing part.

## Typical usage:
| RAM | Used for |
|---|---|
| DRAM | main memory |
| SRAM | cache memory |
