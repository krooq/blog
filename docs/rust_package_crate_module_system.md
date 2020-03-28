# Rust package/crate/module system
##### Mar. 28, 2020 &middot; Gavin Rossiter

So you're learning Rust and you are mega confused about the package/crate/module system? 
Or maybe you are trying to *import* a file and dont understand why the compiler cant find it?

If so this might be the right tutorial for you.

*Note: Pre 2018 editions of Rust work slightly different, [see [1] if you come from pre 2018 Rust](https://doc.rust-lang.org/edition-guide/rust-2018/module-system/path-clarity.html).*

![alt text](images/cargo.png)

In Rust the package/crate/module system is similar to a traditional file system.
There are 3 main concepts...

### Package
Your project is a package.

A package is a collection of crates that forms a set of functionality and it...
- must contain at least one crate
- can contain at most one library crate
- can contain many binary crates
- must have a Cargo.toml 

### Crate
A crate is a logical collection (a tree actually) of modules that forms either a library or compiles to a binary.
- A **library** crate is formed implicitly with the presence of a *src/lib.rs* file.
- A **binary** crate is formed either 
  - implicitly with the prescence of a *src/main.rs* file 
  - explicitly by *src/bin/file-name.rs* files and a declaration in the package Cargo.toml

These files are known as the **crate root** as they form the entry point for the compiler for the crate.

### Module
A module is a compilation unit and a namespace.

You can define a module either
- explicitly as a block e.g. `mod { //... }`
- implicitly as its own file

You can declare a module called *my_module* to be part of a crate by writing `mod my_module;` in
- a *mod.rs* file in the same folder as the module 
- a **crate root** in the same folder as the module

Declaring a module lets the compiler know to compile the module when compiling the crate.
Each module can only be declared once in a crate since a crate is a tree of modules.
If you want your module accessible outside of the declared module, you need to use the `pub` keyword.

#### Using a module
Remember that the Rust package/crate/module system is like a file system.
- You can bring a module into a scope with `use` and the `::` syntax as if it was a file path
- The `crate` keyword is equivalent to `/` i.e. the 'root directory' identifier
- The `super` keyword is equivalent to `../` i.e. the 'one level up' identifier
- The module counts as a "directory" so one level up is the *mod.rs* adjacent to the module file

#### Example
```
src
|
|- a
|  |- a1.rs
|  |- a2.rs
|  |- mod.rs // contains 'pub mod a1;' and 'mod a2;'
|- b
|  |- b1.rs
|  |- mod.rs // contains 'pub mod b1;'
|  
|- main.rs
```
src/a/a1.rs
```
pub fn fn_a1(){ // ... }
```
src/a/a2.rs
```
use super::a1::fn_a1; // Can use the 'super' prefix
// use crate::a::a1::fn_a1; also works

pub fn fn_a2(){
  fn_a1(); // Access to a1 in a2
}
```
src/b/b.rs
```
use crate::a::a1::fn_a1; // Can use the 'crate' prefix
// use super::super::a::a1; also works

pub fn fn_b1(){
  fn_a1(); // Access to a1 in b1
}
```
src/main.rs
```
mod a;
mod b;
use a::a1::fn_a1; // no need to use the 'crate' prefix in the crate root, have a think why if this isn't obvious

fn main() {
  fn_a1(); // Access to a1 in a binary crate root
  b::b1::fn_b1(); // You can also inline module prefixes if you want
}
```

## References
1. [Rust 2018 module system changes](https://doc.rust-lang.org/edition-guide/rust-2018/module-system/path-clarity.html)
2. [Rust book - packages, crates and modules](https://doc.rust-lang.org/book/ch07-00-managing-growing-projects-with-packages-crates-and-modules.html)
3. [Steve Donovan intro to modules](https://stevedonovan.github.io/rust-gentle-intro/4-modules.html)

## Disclaimer
These are things I have learnt on my Rust journey, they could be out of date or just blatantly wrong. I have mentioned my references as extra resources however any mistakes are mine and mine alone, if you see a mistake please let me know so I can correct it.

## Thanks
Thanks to [seri](https://github.com/seritools) who promptly reviewed this tutorial when I asked for help in the Rust discord.