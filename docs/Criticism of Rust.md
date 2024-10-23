> ⚠️: **Trigger Warning**: I know Rust is a well loved language by those that use it and clearly it is useful in some areas considering its wide adoption. I haven't used Rust extensively and keep in mind these are just my opinions.

*There are two kinds of languages, those that solve a problem and those that prove a point, the latter goes to die.*
~ Bjarne Stroustrup, I think

Rust proposes a new system of memory management, one based on ownership and borrowing. Kitty rails set in place as if I don't know how to properly allocate my own bytes. Many would consider it a skill issue of not knowing C. 

If writing software for embedded systems, such as a microcontroller/IOT device, TinyGo has the same performance as Rust as found in this [research paper](https://www.mdpi.com/2079-9292/12/1/143). If you can write Go instead of Rust and get the same performance, the answer is clearly the simpler language.

[65%](https://www.jetbrains.com/lp/devecosystem-2023/go/) of Go Developers use the language for work, vs [20%](https://www.jetbrains.com/lp/devecosystem-2023/rust/) of Rust developers. This means the majority of those learning and writing software in Rust are doing so as a hobby for personal/side projects. Go on the other hand is used by professionals in the industry. This is because Go solves several real world problems, one being code maintainability. Becuase the language is intentianally minimal with features and emphasizes readability, a code base could be untouched for 10 years after the original author left the company and still be maintained or refactored with minimal hassle.  

todo:
it's overly complex. 
no video made yet

TLDR: Just write C, if not then Go or TinyGo for Microcontrollers where low-power and efficiency is needed. 