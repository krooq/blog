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

- You can declare a *module* either
  - explicitly as a block e.g. `mod { //... }`
  - implicitly as its own file

You can add a *module* to a *crate* by writing `mod module-name;` (i.e. the filename without '.rs' extension) in a *crate root*. This will let rustc know to compile the *module* when compiling the *crate*;

You can bring some of a *module* into a scope with `use` and the `::` syntax.
To disinguish your *modules* from other *modules* you need to use the `crate` keyword.  You will also need to use the `pub` on anything in your *module* that you want accessible from other *modules*
e.g.
```
// module_a.rs

pub fn fn_a(){
  // ...
}
```
```
// module_b.rs

use crate::module_a::fn_a; // I needed to use the 'crate' prefix here to find module_a

pub fn fn_b(){
  fn_a(); // yahoo I can call fn_a from module_b
}
```
```
// src/main.rs

mod module_a;
mod module_b;
use module_a::fn_a; // no need to use the 'crate' prefix in the crate root

fn main() {
  fn_a();
  module_b::fn_b(); // I can also inline module prefixes
}
```

## References
- https://doc.rust-lang.org/book/ch07-00-managing-growing-projects-with-packages-crates-and-modules.html
- https://doc.rust-lang.org/edition-guide/rust-2018/module-system/path-clarity.html
- https://stevedonovan.github.io/rust-gentle-intro/4-modules.html

## Disclaimer
These are things I have learnt on my Rust journey, they could be out of date or just blatantly wrong.  If you see a mistake please let me know so I can correct it.