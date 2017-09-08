Statically Linked Executable (elf executable)
=============================================
Most of the time you have to take your executable built in 1 machine and run other machine. 
Sometimes for specific applications like embedded and real time machines, 
the destination m/c are really small and might not have all the standard libraries (like gcc libraries) installed. 

In such case, the executable will not run and fail with error message lib-c not found.
To avoid this we can link all the required library functions along with the executable. 
gcc allows this feature by adding additional option during compilation.

For example:

      $ gcc test.c -o test.o -static

Here, the **'-static'** option will statically link all the referred routies and pack in **test.o**


There are other static link options for linking specific libraries like:

      -static-libgcc
      -static-libstdc++
      -static-libasan
      -static-libtsan
      -static-liblsan
      -static-libubsan

## More details:
http://gcc.gnu.org/onlinedocs/gcc/Link-Options.html
