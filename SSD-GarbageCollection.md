Garbage Collection Algorithms for SSDs
===========================
We all know SSDs (solid-state drives) are block type devices - as the transfer units in a typical SSDs block similar to disks. The major difference in accessing the block information from SSD comes from the physics of the device type, which limits the no.of writes to a particular block (typically a maximum of 10000 writes per memory cell) and also the any overwrite can be done only after erasing the earlier content.
In SSDs we access Data in units called pages (equivalent to disk block size) and memory is erased in larger units called blocks (made up of multiple pages). During erasure process, if the data in some of the pages of the block have valid data - then that block is read and re-written into another previously erased empty block. Then the free pages left by not moving the stale data are available for new data. This is a process called garbage collection (GC) in SSDs

We have intelligent SSD device controllers implementing various Garbage collection techniques which will ensure the long life of devices by reducing the Write Amplification of the device. Write amplification (WA) is an undesirable phenomenon associated with flash memory and  SSDs, where the actual amount of physical data written is much more than the intended data. This happens because flash memory must be erased before it can be rewritten, the process to perform these operations results in moving data/metadata more than once. This multiplying effect increases the number of writes required and hence the name Write Amplification.
The efficiency of the algorithm used to pick the next best block to erase and rewrite can reduce write amplifications drastically and hence better "Garbage Collection" algorithms are really critical.

## Useful Resource:
http://en.wikipedia.org/wiki/Write_amplification
