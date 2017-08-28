
RCU for synchronization
========================

Read-Copy-Update(RCU) is way of implementing wait-free synchronization between multiple processes/threads. 
It works well in multiple reader and writer scenarios (especially ready heavy scenario).


The key idea in RCU is doing an write/update operation in 2 steps
1. Removal step
2. Reclaim step

## Removal step ##
we have to remove references to data items in a data structure after replacing them with references to updated versions of them during this step readers are allowed to read data structure. 
The concurrent access of readers during the remove step will utmost result in some of the readers viewing older version and some view the new version of the data structure.

## Reclaim step ##
we reclaim space of the data items removed from the data structure. There is possibility that removing the old data items can disrupt any readers concurrently referencing those data items. 
Hence the reclaim step cannot start until no reader hold references to those data items of the data structure. For example an updated single node in a RCU linked list cannot be claimed until all the readers don't have any reference to its old version of it.

## So, how it is different? ##
From process synchronization point no reader process has to wait for the writer process. 

But the writer process has to wait till all the readers active during the removal step complete accessing the data item it updates.
The blocking of writer process is implementation dependent. 

Important thing to notice is that the writer process doesn't care about the readers accessing the data item after the removal step, 
because they will see/access the new version of the data item.

RCU's ability to concurrently allow **single write and multiple reads** is unique compared to the conventional locking primitives 
or reader-writer locks. RCU ensures this by maintaining **multiple versions of objects** and ensuring that they are not freed up until all preexisting read-side critical sections complete.

---------------------

## RCU APIs in Linux ##

Read-copy update (RCU) was added to the Linux kernel in October 2002. 
By 2008, there were almost 2,000 uses of the RCU API in the Linux kernel. 
By march 2014, there were more than 9,000 uses.

The core APIs exposed in **'liburcu'** are:

* **rcu_read_lock():** It is used by Reader to mark a RCU-protected data structure. It won't be reclaimed for the full duration of that critical section.

* **rcu_read_unlock():** It is used by Reader to inform the reclaimer that the reader is exiting in a RCU read-side critical section.

* **synchronize_rcu():** It is used by Writer/Updater to block until all pre-existing RCU read-side critical sections on all CPUs have completed. Important thing is that this will not wait for any subsequent RCU read-side critical sections to complete.

* **rcu_assign_pointer():** It is used by Writer to assign a new value to RCU-protected pointer for safely changing its value from the writer to the reader.

* **rcu_dereference():** The reader uses rcu_dereference to fetch an RCU-protected pointer, which returns a value that may then be safely dereferenced. It ensures either the old or new version of the data item.


## For more details: ##
http://en.wikipedia.org/wiki/Read-copy-update
