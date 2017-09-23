TOFS (Text Only File System)
==========================
Text files or flat files are very common and used everywhere. 
Find a substring/pattern match inside the text file is one of the rudimentary operation. 
This operation is also referred to as **‘full text search’**. 
There is no way you can do this without scanning the entire file at least once. 

Since the files are stored in some persistent storage, scanning the entire file will incur lot of I/O. 
One of the biggest design decision in any system is to avoid IO overhead.
We are proposing an alternative to existing text search mechanism, which can do it without scanning the complete file. 
Hence, avoiding the IO overhead involved in text search.

The proposed file system (TOFS) is much like a Linux based EXT2 file system with a persistent cache module, 
a new system call ‘search’ and modified ‘write’ system call. The persistent cache module is stored as a flat file in file system. 
It has 2 in-memory component which stores the most frequently used keywords/phrases.

1. Hash table storing words and phrases of file.
2. Simple key-value based LRU cache (storing index of the words pointed in above table as key and list of inodes having them as value).

--------------------------

For any text search, the in-memory cache will always be referred and the list of matching files will be returned without 
scanning the file content. Hence, a ‘full text search’ can be done in *O(1)* irrespective of the file size and no.of files in the file system.

For any text search, the in-memory cache will always be referred and the list of matching files will be returned without scanning the file content. Hence, a ‘full text search’ can be done in O (1) irrespective of the file size and no.of files in the file system.

Whenever a text search is made,
1. Hash of the given ‘keyword/sentence’ is calculated
2. Calculated hash value is used to refer in the Hash table
3. If an entry is found
   - Index of the entry is obtained from hash table
   - LRU cache is referred for the matched index to get the list of matching file inodes
   - List of files corresponding to the inodes are returned.
4. In case of miss – ‘NO MATCH FOUND’ error message is returned.


  Note: TOFS can be mainly for string text files/flat files. Performance on other file types may be really bad or sometimes the system may crash. We need to implement error checks to ensure only text files are being stored.
