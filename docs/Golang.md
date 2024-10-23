### History and Overview

In 1970 Dennis Ritchie created a high level language called C to build the Unix operating system, previously written in assembly. Unfortunately passing away before the creation of Go, his colleagues Ken Thompson and Rob Pike developed Go, a modern C of the 21st century, publically released as open source in 2012. Modern object oriented languages continue to add eachothers features in an attempt to keep market share. This means they are growing in complexity while simultaneously becoming more similar to one another. This is _bloat without distinction_.  

Go is an unapologetic boring language with an intended lack of features. This means code is written procedurally in a simple fashion. A single programmer could write an entire codebase, leave for 5 years, and his coworkers will easily pick up where he left off. Writing in Go means large code bases are readable. Files are read top to bottom without hunting down where a method is imported from, or traversing several files to find the original implementation in a nest of inheritance.

### Problems of C Addressed With High Level Features

Though required to manage if absolute performance is necessary, the following are the main problems with writing code in C:

1. Uninitialized variables
2. Out-of-bounds
3. Use-after-free
4. Read or write to unintended object (memory safety bug)

Go solves 1 by zeroing out newly created variables, so instead of unexpected behavior in C, Go will return a value of zero. Problem 2 is solved with bounds checking of arrays/slices to ensure index is not out of range. Next, without needing to malloc and free memory by hand, Go's garbage collector takes care of number 3. Finally, number 4 is prevented without the use of pointer arithmetic, though pointers are allowed and encouraged in Go, we cannot manipulate them.

### Learning Resource

Go is intentionally a conservative and minimal language that doesn’t change quickly, however, here are two things to be aware of when reading *The Go Programming Language* book.

- Go Modules Replaced GOPATH
- Generics are not included

Besides this there may be occasional deprecated functions from standard packages such as rand or crypto. Overall it is a highly recommended book as Brian Kerningham is renowned computer scientist, OG Unix developer and also author of *The C Programming Language*. Alan Donovan, co-author, is an engineer in the Go Team at Google.     
[Book PDF](http://www.cs.uniroma2.it/upload/2017/TSC/The%20Go%20Programming%20Language.pdf)
