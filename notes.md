# Learn Rust Programming - Complete Course

# Introduction & Learning Resources
## Course Goals
- Getting familiar with core concepts and syntax
- Data Tyles & Data Structures
- Ownership & Borrowing
- Allocating data to memory and accessing data from memory
- Standard Library
- Generics, Traits, Lifetimes, and more...

## Why Learn Rust?
- Fastest language after C
- Rich type system
- No garbage collector (faster runtime)
- Useful compiler output
- Memory Safety
- Most beloved prog lang since 2016 (Stack Overflow)
- Fast adoption in various branches

# Setup Rust
- Use Rustup: https://www.rust-lang.org/learn/get-started
    - `curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh`
- Let's start with Hello World
    - `cargo new hello_world`
    - Every program in rust starts with main function
    ```
    fn main() {
        println!("Hello, world!");
    }
    ```
    - To build, run `cargo build`
    - To run, run `cargo run`

# Variables
- Assigned using `let` keyword
- Print to standard output by `print!()` or `println!()` macros
- Scope of a variable is defined by the block of code in which it is declared
- Function is a named block of code that is reusable
- Shadowing allows a variable to be re-declared in the same scope with the same name

# Numbers & Binary System 
# Chars, Bools & Unit Types 
# Statements & Expressions 
# Functions 
# Ownership 

# Resources
- https://www.youtube.com/watch?v=BpPEoZW5IiY
- The Rust Programming Langauge (Book)
- Rustlings
- Rust by Example
- Rust by Practice (these notes)