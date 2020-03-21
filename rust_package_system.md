# Rust package system
##### 21th March 2020

Like everything in Rust, the package system smart and simple.
However the documentation is sparse and often out of date which can make it confusing for new rustaceans.
I'll try to explain it as simply as possible.

#### Package
Your project is a `package`.

A `package` is a collection of `crate`s that forms a set of functionality and it...
- must contain at least one `crate` 
- can contain at most one `library crate`
- can contain many `binary crate`s
- must have a Cargo.toml
  

#### Crate
A `crate` is a logical collection (a tree actually) of `module`s that forms either a library or compiles to a binary.
- A `library crate` is formed implicitly with the presence of a src/lib.rs file.
- A `binary crate` is formed either 
  - implicitly with the prescence of a src/main.rs file 
  - explicitly by src/bin/\<file\>.rs files and a declaration in the `package` Cargo.toml.


#### Module
A `module` is a namespace.

- You can declare a `module` either
  - explicitly as a block e.g. `mod { //... }`
  - implicitly as its own file

You can add a `module` to a `crate` by writing `mod module-name` (i.e. the filename without '.rs' extension) in any `module` that is alredy part of the `crate` such as the implicit `module` src/main.rs. 

You can bring some of a `module` into a scope with `use` and the `::` syntax.

## References
https://doc.rust-lang.org/book/ch07-00-managing-growing-projects-with-packages-crates-and-modules.html