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
## Numbers - Integer Types
- Signed integer: Can represent both positive and negative integers
- Unsigned integer: Always positive integers

    | Length  | Signed | Unsigned |
    |---------|--------|----------|
    | 8-bit   | i8     | u8       |
    | 16-bit  | i16    | u16      |
    | 32-bit  | i32    | u32      |
    | 64-bit  | i64    | u64      |
    | 128-bit | i128   | u128     |
    | arch    | isize  | usize    |
- Note arch is computer architecture so probably 64 bit
## Numbers - Default Types
- Integers: `i32`
- Floats: `f64`
## Numbers - Binary Number Systems
- Consider  `42`
    - 2 would be in 1's place and 4 would be in the 10's place
    - $(4 \times 10^1) + (2 \times 10^0)$
    - $= (4 \times 10) + (2 \times 1)$
    - $= 40 + 2 = 42$
- But in computers, things look different than decimal
    - `42` in binary is `00101010`
    - There are 8 bits in 1 byte
    - We have the same logic as above, but with a base of `2`

    | 0 | 0 | 1 | 0 | 1 | 0 | 1 | 0 |
    |---|---|---|---|---|---|---|---|
    | $2^7$ | $2^6$ | $2^5$ | $2^4$ | $2^3$ | $2^2$ | $2^1$ | $2^0$ |
    | 128 | 64 | 32 | 16 | 8 | 4 | 2 | 1 |

    - $(1 \times 2^5) + (1 \times 2^3) + (1 \times 2^1)$
    - $= (1 \times 32) + (1 \times 8) + (1 \times 2)$
    - $= 32 + 9 + 2$
    - $= 42$
## Numbers - Range of 8-bit integers
- Smallest possible 8-bit integer (unsigned): `0`
- Largest possible 8-bit integer (unsigned): `255`
    - Why? Because if there are 8 positions, then $2^7 + 2^6 + ... + 2^0 = 255$
- Need something larger than 255? Then add more bits to store it
    - 16-bit unsigned integer can store `2^16 => 65,535`
## Numbers - Signed Integers
- Two's complement 
    - The processor will take a number (42)
    - Then it will invert the binary number 
        - $00101010$
        - $11010101$
        - After inverting the number, we add one single bit
        - in this case, this becomes a 0 and we have a carry of 1
        - $11010110$
        - `-42`
    - Note that the sign bit, the farthest left shows if the number is positive or negative
        - A `1` means negative; `0` is positive
## Numbers - usize & isize
- Architecture dependent
- On 32-bit architecture: `32-bit`
- On 64-bit architecture: `64-bit`
- Pointer sized integer type because it matches the size of a `word` in a given platform
## Numbers - What is a word?
- Processor does not read 1 byte at a time from memory, it reads 1 word at a time
- In a `32-bit` processor it can access 4 bytes (32 bits) at a time
- In a `64-bit` processor it can access 8 bytes (64 bits) at a time
- `usize` gives you the guarantee to be always big enough to hold __any pointer__ or any offset in a data structure
## Numbers - Floating Point
- `f32` - size of 32 bits
- `f64` - size of 64 bits
- Representation according to IEEE-754 specification
## Numbers - Boolean Logic
- Boolean logic deals with values that are either "true" or "false" (1 or 0)
- Three basic operations: AND, OR, NOT
    - AND
        - f && f => f
        - f && t => f
        - t && f => f
        - t && t => t
    - OR
        - f || f => f
        - f || t => t
        - t || f => t
        - t || t => t
    - NOT
        - !false => true
        - !true => false
## Numbers - Bitwise Operations
- Operations that manipulate individual bits that make up a binary number
- Treating each bit of a bunary number as a separate unit and perform logical operations on them
- AND, OR, XOR, bitwise shifting
### Numbers - AND (&)
- AND returns 1 only when __both__ of its inputs are 1
- Truth Table

| A | B | Q |
|---|---|---|
| 0 | 0 | 0 |
| 0 | 1 | 0 |
| 1 | 0 | 0 |
| 1 | 1 | 1 |

### Numbers - OR (|)
- OR returns 1 only if __at least one__ of its inputs is 1
- If both inputs are 0, the output will also be 0.
- Truth Table

| A | B | Q |
|---|---|---|
| 0 | 0 | 0 |
| 0 | 1 | 1 |
| 1 | 0 | 1 |
| 1 | 1 | 1 |

### Numbers - XOR (^)
- XOR returns 1 if the inputs are __different__
- If both inputs are the __same__, the output will be 0.
- Truth Table

| A | B | Q |
|---|---|---|
| 0 | 0 | 0 |
| 0 | 1 | 1 |
| 1 | 0 | 1 |
| 1 | 1 | 0 |

### Numbers - Bitwise Left Shift
- `1 << 5`
- `00000000` => `00100000 => 32`
### Numbers - Bitwise Right Shift
- `0x80 >> 2 = 128 >> 2`
- `10000000` => `00100000 => 0x20 => 32`

# Chars, Bools & Unit Types 
## Char
- `char` is a single character of size 4 bytes and can store all unicode values
- `char` is represented like `'c'`
- Strings use double quotes

## Bool
- Boolean value can be either `true` or `false`
- bool is of size 1 byte
- Negation with `!`
## Unit type
- The unit type is an empty tuple of size 0 bytes, used to return "nothing" in expressions or functions
- Example:
    - `let _v: () = ();` // unit represented as empty tuple

# Statements & Expressions 
# Functions 
# Ownership 

# Resources
- https://www.youtube.com/watch?v=BpPEoZW5IiY
- The Rust Programming Langauge (Book)
- Rustlings
- Rust by Example
- Rust by Practice (these notes)