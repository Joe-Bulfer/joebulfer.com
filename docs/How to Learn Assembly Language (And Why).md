> 📹 **Related Video**: Watch the related video to this article [here](https://www.youtube.com/watch?v=xpNWmf_-Pj0).


### TLDR


#### HOW

- lc3tutor.org for web based simulator and code snippets
	- or LC3Tools for a desktop application simulator
- Introduction to Computing Systems Book, written by LC-3 creator

#### WHY

- Gain appreciation of how computers work and shoulders of giants we stand on.
- Optimization scenarios such as digging into x86 of high level language to prevent bounds checking.
- There are few jobs where people write in assembly relative to high level languages, but they are compilers/toolchain developers, malware analysts, embedded development, and computer science teachers.

### How I learned Low Level Stuff

Machine Organization is an upper level Computer Science course at my university. Dreaded by many, understanding the computer down to the transistor is necessary as well as designing logic gates and writing assembly code. Programming in high level languages (which is all most know how to do) does not help prepare. The course starts with character and number representation in binary, as well as arithmetic operations (add, subtract) and logical operations (AND, OR). After we understand base 2 and can perform basic operations, Circuit Verse was introduced to build logic gates. Our final culmination was an [ALU](https://circuitverse.org/users/216644/projects/alu-6a89d8d5-6504-4ca4-b9c0-c85d66eb6966) (Arithmetic Logic Unit), which is the heart of the CPU. After CircuitVerse, LC-3 was introduced.

### LC-3

LC-3 is a simulated instruction set architecture (ISA) and assembly language designed for educational purposes. It is hypothetical does not run on actual hardware as most ISAs do. Instead there are several simulators available. One is [LC3Tools](https://github.com/chiragsakhuja/lc3tools), a desktop application which requires an install. On Linux I downloaded a single AppImage and it worked flawlessly. Alternatively, there is a web based simulator on [lc3tutor.org](http://lc3tutor.org/), as well as many great example code snippets demonstrated in the video.

If you would like to gain an understanding of an even lower level than assembly to start from a truly bottom up approach, you can learn binary and build logic gates on [CircuitVerse](https://circuitverse.org). This will help in understanding the inner working of LC-3, but is not necessary.

Though very dense at nearly 800 pages, the [textbook](https://icourse.club/uploads/files/96a2b94d4be48285f2605d843a1e6db37da9a944.pdf) written by the original LC-3 creator is available. This was the reading material in my Machine Organization course, though most students only opened it up when they needed to reference an opcode.
