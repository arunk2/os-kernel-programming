Object Oriented programming in OS Kernel
========================================
### Kernel/Device drivers development - 'Abstraction'
One of the core concept in object oriented paradigm is 'Abstraction'. 
As most of us know Abstraction is nothing but hiding complete technical details (how its implemented or working) 
from user (client code using the system/object/module) 
and exposing only necessary details for interacting with system/object/module.

I guess many of us regularly use **static functions and variables** which have a file level scope, while Kernel/Device drivers programming. 
Although there are other reasons like to **avoid compilation errors of having same function names** in different modules.

From a design point of view - I would say this as **'Abstraction'**. 
Here we declare all the unwanted rather internal only functions and variables of system as static. 
We can equate them to the **private member functions and variables** in any OOPS implementation. 
And we typically use **EXPORT_SYMBOL** to expose functions and variables across the system.
We can equate them to the **public member functions and variables** in any OOPS implementation.

With more and more **Object based File system** and other subsystem being implemented I guess it will not be a bad idea for kernel developers to spend some time in OOAD.

Even though the following links are not directly related to above discussion, they might give some ideas on ways of OOP in C language.
- http://www.planetpdf.com/codecuts/pdfs/ooc.pdf
- http://stackoverflow.com/questions/674722/struggling-with-c-coming-from-object-oriented-land?rq=1
- http://stackoverflow.com/questions/19209455/data-abstraction-in-c
