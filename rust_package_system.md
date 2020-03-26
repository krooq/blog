# Rust package system
##### 21th March 2020

Like everything in Rust, the package system smart and simple.
However the documentation is sparse and often out of date which can make it confusing for new rustaceans.
I'll try to explain it as simply as possible.

### Package
Your project is a *package*.

A *package* is a collection of *crates* that forms a set of functionality and it...
- must contain at least one *crate*
- can contain at most one *library crate*
- can contain many *binary crates*
- must have a Cargo.toml
  

### Crate
A *crate* is a logical collection (a tree actually) of *modules* that forms either a library or compiles to a binary.
- A *library crate* is formed implicitly with the presence of a src/lib.rs file.
- A *binary crate* is formed either 
  - implicitly with the prescence of a src/main.rs file 
  - explicitly by src/bin/file-name.rs files and a declaration in the *package* Cargo.toml.

These files are known as the *crate root*.

### Module
A *module* is a compilation unit and a namespace.

- You can define a *module* either
  - explicitly as a block e.g. `mod { //... }`
  - implicitly as its own file

You can declare a *module* to be part of a *crate* by writing `mod module-name;` (i.e. the filename without '.rs' extension) in a *mod.rs* file or a *crate root* in the same folder as the *module*. This lets rustc know to compile the *module* when compiling the *crate*.
Each *module* can only be declared once in a *crate*.

You can bring some a *module* into a scope with `use` and the `::` syntax. You will also need to use the `crate` and `super` keywords to select internal *modules* in preference to external *modules*.

- To access your *module* **inside** the *module* it is declared in you must
  - declare as `mod module-name;`
  - bring into scope with `use super::my_module::*;`
- To access your *module* **outside** the *module* it is declared in you must
  - declare as `pub mod module-name;`
  - bring into scope with `use crate::my_module::*;`

##### Example
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
```
// src/a/a1.rs
pub fn fn_a1(){
  // ...
}
```
```
// src/a/a2.rs
use super::a1::fn_a1; // Must use the 'super' prefix

pub fn fn_a2(){
  fn_a1(); // yahoo I can access fn_a1 in a2.rs
}
```
```
// src/b/b.rs
use crate::a::a1::fn_a1; // Must use the 'crate' prefix

pub fn fn_b1(){
  fn_a1(); // yahoo I can access fn_a1 in b1.rs
}
```
```
// src/main.rs
mod a;
mod b;
use a::a1::fn_a1; // no need to use the 'crate' prefix in the crate root

fn main() {
  fn_a1();
  b::b1::fn_b1(); // I can also inline module prefixes
}
```

## References
- https://doc.rust-lang.org/book/ch07-00-managing-growing-projects-with-packages-crates-and-modules.html
- https://doc.rust-lang.org/edition-guide/rust-2018/module-system/path-clarity.html
- https://stevedonovan.github.io/rust-gentle-intro/4-modules.html

## Disclaimer
These are things I have learnt on my Rust journey, they could be out of date or just blatantly wrong.  If you see a mistake please let me know so I can correct it.