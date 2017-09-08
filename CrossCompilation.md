Cross Compilation
=================

## What is Cross Compilation?
Typically any desktop or server application have almost the same development platform (CPU + OS - that runs your build) 
and the target platform (CPU + OS - that runs your production application) are the same. 
Platform is nothing but the combination of CPU architecture, and Operating System. 

### Definition:
The process of building an executable binaries on a platform, and run them on another platform is called "cross compilation". A special compiler is needed for doing cross compilation that is called "cross compiler" or "toolchain".  For example, desktop PC application developers for Windows or Linux can build and run their binaries on the very same machine. Even developers of server applications generally have the same basic architecture and Operating System on both their development machine and server machine. The compiler used in these cases is called "native compiler".
Usually Application built for non-PC architecture (like embedded application running on ARM, PowerPC, MIPS architectures) use a cross compiler to generate an executable binaries. 
Cross Compilers must be specifically tailored for doing cross-compilation from the development machine (host), to embedded machine (target).

----------------------------------------------------

## Cross Compilation Example - for MIPS R3000/Linux

I would like to share a Cross compiler toolchain, which worked for me. 
I was trying to cross compile into a MIPS R3000 + Linux patform. 
Following are the steps in getting the cross compiler up and running.

1. Download the latest version of crosstool-ng

        wget http://crosstool-ng.org/download/crosstool-ng/crosstool-ng-VERSION.tar.bz2

2. Extract it

        tar xjf crosstool-ng-VERSION.tar.bz2

3. Get into extracted dir

        cd crosstool-ng-VERSION

4. Build the cross tool chain (give the place where u want crosstool should get compiled/install into)

        ./configure --prefix=/some/place
        make
        make install

5. Add the path to global PATH variable so that all executables are visible
    
        export PATH="${PATH}:/some/place/bin"

6. Now, you have created the crosstool-ng setup. Let us do the actual toolchain for required paltform.
create a directory to work in, then list the existing samples (pre-configured toolchains that are known to build and work) to see if one can fit your actual needs. example is 'mips-unknown-linux'.

        mkdir /your_toolchain
        cd ~/your_toolchain
        ct-ng list-samples
        ct-ng show-mips-unknown-linux

7. Configure ct-ng to use it then build it:

        ct-ng mips-unknown-linux
        ct-ng build

8. Its all done, you can set access to your toolchain, and call your new cross-compiler with :
    
        export PATH="${PATH}:~/your_toolchain/mips-unknown-linux/bin"


We call access the cross compiler gcc tools with corresponding prefix. 
For example gcc can be called with **'mips-unknown-linux-gcc'** at command prompt.



## For more details:
http://crosstool-ng.org/
