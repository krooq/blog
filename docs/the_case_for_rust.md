# The case for Rust
##### Mar. 15, 2020 &middot; Gavin Rossiter

## Introduction
Have you ever tried learning a lower level programming language after working almost exclusively with a modern high level languages like Python/Ruby, Javascript or even Java/C#?
If you have then you will probably know the feeling all too well of being lost in a strange world full of things you heard tales of but never had to actually deal with.  Things like memory allocation and deallocation, the stack and the heap and pointers.

I use Java at my day job and it's a great language, it's a real workhorse, fast, statically typed, readable and relatively simple. In Java the JVM handles all of these low level details so we can get to work quickly and avoid the nasty bugs low level programming can introduce.  In doing so we sacrifice a bit of performance and control but usually we consider that acceptable on modern hardware.  
Python is still the fastest growing language as of 2019 in terms of popularity which is due mostly to its simplicity.  Just like in Java, Python users need not worry about memory allocation or garbage collection, it's all handled by the runtime, just write code and get work done!
This is great for scripts but if you want to write a program that is fast all round you can't use Python.
You could use Java, it's pretty fast but if you want to do anything low level like graphics you will end up calling some bare metal C/C++ library that has direct access to system calls and hardware.

It's the same for most other modern high level languages. 
We think of these languages as being more advanced, an evolution from the clunky procedural C from the 70s.  We say that these high level languages let us think with a higher level of abstraction which lets us create more complex, maintainable systems. We say they allow us to better utilize our thinking for functional features over technical mechanics.

## ... But do they?

For the past few weeks I have been learning Rust, a modern multipurpose, low level language. Rust is brimming with modern features inspired from higher level languages. However Rust's killer feature combo is it's C-level performance and compiler enforced memory safety.
As of 2019, the Stack Overflow developer survey shows Rust as the most loved programming language for the 4th year in a row, meaning the people using Rust don't want to stop using Rust.
I find this quite interesting for a few reasons.
1. Rust has a steep learning curve.  The low level memory safety introduces a new concept to programmers where one must be quite explicit about the lifetime of each variable. It's a feature unique to Rust and is quite diffuclt to get used to if one comes from a higher level language.
2. The next languages on the most loved list are Python then TypeScript. I feel like these languages are here because they serve a unique niche and they serve it well. 
Python is excellent for numerical analysis and has first class libraries for machine learning.  The simplicity is also very alluring to new developers.
TypeScript on the otherhand is the type safety that web developers have been begging for since web applications started to become fully fledged complex programs.

## Some of them do... most of them do not.

### Python
I think it is undeniable that Python is simple to read and easy to learn.
If you are an academic or data scientist that writes scripts to do analysis that'll get thrown away next week (or at the end of your PhD), Python is for you. Python looks to be the go to language to write scripts that can do actual things, mostly because it is easy to call C code from Python if you need to do a long task that you dont want to take too long. Python is for scripts.

### TypeScript
If you are a web developer working on a large scale web application with lots of other developers, TypeScript is good choice.  Whether actually making any large scale web application is the right choice is debatable.
The web is the logical place for virtualized languages, Java was actually made for the web, y'all remember them applets?  If you don't know where it will run then VMs make sense but obviously that limits you to what the VM can actually do. Web languages are languages that get interpreted by other programs like a browser, they are meant to be dynamic, expressive, powerful, lightweight and adaptable. They are not meant to make someones computer do arbitrary hardware dependent or high performance tasks.

### Rust
If you are not either of those things then the best choice is a bare metal language.
At the end of the day, there will come a point where you will need to know how to tricky low level things.
It would be better if we all just wrote programs that compile to executables so we can run them natively.
It would be better if we only had to write in one programming language that could do it all.
It would be better if our programs were as fast as possible.

For these things one needs:
A language that can run hella fast.
A language that lets you ask the hardware drivers (or OS) to do things directly.
A language that lets you control every detail that you might need to because at some point, you will need to.
A language that doesn't run in an environment that does stuff you didn't ask it to do.

That language Rust (or C/C++ or maybe GO).

## So what about Java, why does still even exist?
At the start I said Java was a great language, and it is.  But I don't think it's the best language.
Software suffers from a great plague, "it exists therefore we must use it".
Lots of software is already written in Java and it still works so we teach engineers to learn Java so the software can be extended and maintained which makes Java a good choice for business because it has long term support and a big workforce.  The irony of this of course is that the JVM is written in C.
One of the reasons the JVM still exists because some operating systems (looking at you Windows) can't get on board a standard like POSIX.
Standards are fantastic if used at the correct level. For example, at the hardware level, graphics driver standards like OpenGL give the programmer a uniform API to use so no matter what GPU they program for, if it implements the standard (which most do) then the program will work.  But of course Microsoft (and Apple) think they are holy and have their own standard DirectX/Metal which means GPU manufacturers have to write drivers for this standard too.
This cross platform support that the VM provides is good on paper as it gives the programmer a virtual standard to program against but in reality each platform will do something different anyway which can be a pain for the developer to work around.

## References
- https://insights.stackoverflow.com/survey/2019#most-loved-dreaded-and-wanted
- https://www.rust-lang.org/