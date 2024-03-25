write hello world in rust:

```
fn main() {
	println!("hello rust!");
}
```

`fn` -> declare a function
`!` -> macro
### Cargo - rust's build system

`cargo new` -> generate a new cargo project
`cargo new --vsc=git` -> generate cargo project with git
`cargo init` -> initialise a cargo project

`cargo build` -> builds a project
`cargo run` -> run the binaries generated after build
`cargo check` -> check your code, make sure it compiles without actually generating an executable

### Variables
By default, variables in rust are immutable and strongly typed, but you can make them mutable using `mut` keyword.

```
let x = 10;     // immutable
let mut x = 10; // mutable
```
