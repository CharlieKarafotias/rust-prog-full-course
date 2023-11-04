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

## Exercises
1) A variable can be used only if it has been initialized
    ```
    // Fix the error below with the least amount of modifications to the code
    fn main() {
        let x: i32; // uninitialized but used, ERROR !
        let y: i32; // Uninitialized but also unused, only a Warning !

        assert_eq!(x, 5);
        println!("Success!");
    }
    ```
    - To fix this, lets initialize x; `let x: i32 = 5;`
    - To fix the warning of `y`, you can use `_y` to mute it
2) Use `mut` to mark a variable as mutable
    ```
    // Fill the blanks in the code to make it compile
    fn main() {
        let __ __ = 1;
        __ += 2; 
        
        assert_eq!(x, 3);
        println!("Success!");
    }
    ```
    - This can become
    ```
    // Fill the blanks in the code to make it compile
    fn main() {
        let mut x = 1;
        x += 2; 
        
        assert_eq!(x, 3);
        println!("Success!");
    }
    ```
    - Note that the type for `x` here is `i32`
3) A scope is the range within the program for which the item is valid
    ```
    // Fix the error below with least amount of modification
    fn main() {
        let x: i32 = 10;
        {
            let y: i32 = 5;
            println!("The value of x is {} and value of y is {}", x, y);
        }
        println!("The value of x is {} and value of y is {}", x, y); 
    }
    ```
    - Notice there is a block scope here where `y` is initialized
    - This won't compile because a variable is only available inside the scope it was declared
    - Solution: 
    ```
    // Fix the error below with least amount of modification
    fn main() {
        let x: i32 = 10;
        let y: i32 = 5;
        {
            println!("The value of x is {} and value of y is {}", x, y);
        }
        println!("The value of x is {} and value of y is {}", x, y); 
    }
    ```
4) Fix an error using a function
    ```
    // Fix the error with the use of define_x
    fn main() {
        println!("{}, world", x); 
    }

    fn define_x() {
        let x = "hello";
    }
    ```
    - The problem in `main()` is that we are trying to access a variable `x` that does not exist
    - What we can do is move the `println` inside of `define_x()`
    ```
    // Fix the error with the use of define_x
    fn main() {
        define_x();
    }

    fn define_x() {
        let x = "hello";
        println!("{}, world", x);
    }
    ```
5) You can declare a new variable with the same name as a previous variable, here we can say the first one is shadowed by the second one.
    ```
    // Only modify `assert_eq!` to make the `println!` work(print `42` in terminal)
    fn main() {
        let x: i32 = 5;
        {
            let x = 12;
            assert_eq!(x, 5);
        }

        assert_eq!(x, 12);

        let x = 42; // Shadowed
        println!("{}", x); // Prints "42".
    }
    ```
    - Notice the variable `x` in the main scope is separate from the `x` in the block scope
    - Further, notice we shadow the main scope's `x` to 42
    - Solution:
    ```
    fn main() {
        let x: i32 = 5;
        {
            let x = 12;
            assert_eq!(x, 12);
        }

        assert_eq!(x, 5);

        let x = 42;
        println!("{}", x); // Prints "42".
    }
    ```
6) 
    ```
    // Remove a line in the code to make it compile
    fn main() {
        let mut x: i32 = 1;
        x = 7; // x = 7
        // Shadowing and re-binding
        let x = x; // 7
        x += 3; // x = 10


        let y = 4;
        // Shadowing
        let y = "I can also be bound to text!"; 

        println!("Success!");
    }
    ```
    - Notice the line `let x = x;`
    - Every variable in Rust is immutable
    - So when we shadow it, it becomes immutable so now `x += 3` will fail
    - Solutions:
        - Can make `let mut x = x;`
        - Can remove `x += 3;`
        - Can remove `let x = x;`
    ```
    // Remove a line in the code to make it compile
    fn main() {
        let mut x: i32 = 1;
        x = 7; // x = 7
        x += 3; // x = 10


        let y = 4;
        // Shadowing
        let y = "I can also be bound to text!"; 

        println!("Success!");
    }
    ```
7) Unused variables
    ```
    fn main() {
        let x = 1; 
    }

    // Warning: unused variable: `x`
    ```
    - 2 solutions
        - change `x` to `_x`
        - another way is to add statement `#[allow(unused_variables)]`
    ```
    #[allow(unused_variables)]
    fn main() {
        let x = 1; 
    }

    // Warning: unused variable: `x`
    ```
8) Destructuring
    - We can use a pattern with `let` to destructure a tuple to separate variables
    ```
    // Fix the error below with least amount of modification
    fn main() {
        let (x, y) = (1, 2);
        x += 2;

        assert_eq!(x, 3);
        assert_eq!(y, 2);

        println!("Success!");
    }
    ```
    - Solution:
    ```
    // Fix the error below with least amount of modification
    fn main() {
        let (mut x, y) = (1, 2);
        x += 2;

        assert_eq!(x, 3);
        assert_eq!(y, 2);

        println!("Success!");
    }
    ```
9) Destructuring assignments
    - As of Rust 1.59, you can now use tuple, slice and struct patterns as the left-hand side of an assignment
    ```
    fn main() {
        let (x, y);
        (x,..) = (3, 4);
        [.., y] = [1, 2];
        // Fill the blank to make the code work
        assert_eq!([x,y], __);

        println!("Success!");
    } 
    ```
    - We can declare 2 variables at once `let (x, y);`
    - We can then destructure the data structures on the right
        - `(x,..) = (3, 4);`
        - we dont need to use the let keyword since we already did that
        - we assign 3 to `x`; `..` means we don't care about the other
        - `[.., y] = [1, 2];`
        - we dont care about the first value of the array; the second value `2` will be placed into `y`
    - Solution:
    ```
    fn main() {
        let (x, y);
        (x,..) = (3, 4);
        [.., y] = [1, 2];
        // Fill the blank to make the code work
        assert_eq!([x,y], [3, 2]);

        println!("Success!");
    } 
    ```

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