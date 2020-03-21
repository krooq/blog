# Rust package system
##### 21th March 2020

Like everything in Rust, the package system smart and simple.

#### Package
Your project is a `Package`.

A `Package` is a collection of `Crate`s that forms a set of functionality and it...
- must contain at least one `Crate` 
- can contain at most one `library Crate`
- can contain many `binary Crate`s
- must have a Cargo.toml
  

#### Crate
A `Crate` is a logical collection of `Module`s that forms either a library or compiles to a binary.
- A `library Crate` is formed with the presence of a src/lib.rs file.
- A `binary Crate` is formed either 
  - implicitly with the prescence of a src/main.rs file 
  - explicitly by src/bin/<file>.rs files and a declaration in the `Package` Cargo.toml.


#### Module
A `Module` is a namespace, just like in Python.
You can declare them as a block or for an entire file using `mod` and bring them into scope with `use`.

## References
https://doc.rust-lang.org/book/ch07-00-managing-growing-projects-with-packages-crates-and-modules.html