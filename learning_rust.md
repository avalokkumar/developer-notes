  ### Introduction


#### Why Rust?
> Rust is a modern systems programming language that provides a number of benefits over other programming languages. Here are some of the reasons why you might want to consider using Rust for your next project:

1. **Memory safety:** Rust's ownership and borrowing model makes it possible to write code that is memory safe, without relying on garbage collection or manual memory management. This can help prevent common memory-related errors like null pointer dereferencing and buffer overflows.

2. **Performance:** Rust is designed to be a fast and efficient language, making it a good choice for systems programming and other performance-critical applications. Its performance is comparable to C or C++, but with greater safety guarantees.

3. **Concurrency:** Rust's ownership model and support for message passing make it well-suited for concurrent programming. Rust's type system and borrowing rules help prevent common concurrency errors like data races and deadlocks.

4. **Expressiveness:** Rust is a modern language with a syntax that is designed to be easy to read and write. Its features, such as pattern matching, closures, and traits, make it possible to write expressive and flexible code.

5. **Growing ecosystem:** Rust has a growing ecosystem of libraries, tools, and frameworks, making it easier to get started with the language and to build complex systems. It also has a vibrant community of developers who are working on a wide range of projects, from web development to embedded systems.
---
#### Basic Programs

* Hello World
```rust
fn main() {
    println!("Hello, world!");
}
```

* Example program in Rust that prompts the user to enter their name, reads the input from the command line, and then prints a personalized greeting:

```rust
use std::io;

fn main() {
    println!("Please enter your name:");

    let mut name = String::new();
    io::stdin().read_line(&mut name).expect("Failed to read line");

    println!("Hello, {}! Nice to meet you.", name.trim());
}

```
### Getting Started

#### Basic Formatting

In Rust, basic formatting can be done using the println! macro, which works similarly to the printf function in C and other languages.

The println! macro takes a format string as its first argument, followed by any number of values to be formatted and printed. The format string is a string literal that can contain placeholders for the values to be printed. 
**Here's an example:**

```rust
let x = 42;
let y = 3.14;
let name = "Alice";

println!("x = {}, y = {:.2}, name = {}", x, y, name);
```

In this example, the format string contains three placeholders:

* {} is a placeholder for the first value, x, which will be printed as an integer.
* {:.2} is a placeholder for the second value, y, which will be printed as a floating-point number with two decimal places.
* {} is a placeholder for the third value, name, which will be printed as a string.

The values to be printed are passed as additional arguments to the println! macro, in the order they appear in the format string.

**Here are some more examples of using the println! macro with various formatting options:**

##### Using the `println!` macro with formatting
```rust
let x = 42;
let y = 3.14159265;
let s = "hello, world!";
let arr = [1, 2, 3];

println!("x = {}", x);                    // x = 42
println!("y = {:.2}", y);                  // y = 3.14
println!("s = {}", s);                     // s = hello, world!
println!("arr = {:?}", arr);               // arr = [1, 2, 3]
println!("arr = {:#?}", arr);              // arr = [
                                           //     1,
                                           //     2,
                                           //     3,
                                           // ]
```


In these examples, the format string contains placeholders for the values `x`, `y`, `s`, and `arr`. The `{:}` syntax is used to format the values as strings, with `{:.2}` used to format the y value as a floating-point number with two decimal places. The `{:?}` syntax is used to format the arr value as a debug string, which prints the array with square brackets and commas. The `:#?` syntax is used to print the array with each element on its own line, indented with two spaces and surrounded by square brackets.


##### Using the `format!` macro and `std::fmt`

The `format!` macro and `std::fmt` module provide a more powerful and flexible way to format values in Rust. 
Here's an example that defines a custom Person struct and implements the `std::fmt::Display` trait to customize how instances of the Person struct are formatted:

```rust
use std::fmt;

struct Person {
    name: String,
    age: u32,
}

impl fmt::Display for Person {
    fn fmt(&self, f: &mut fmt::Formatter) -> fmt::Result {
        write!(f, "{} ({} years old)", self.name, self.age)
    }
}

fn main() {
    let alice = Person { name: "Alice".to_string(), age: 25 };
    let bob = Person { name: "Bob".to_string(), age: 30 };

    println!("{} and {}", alice, bob);
}
```


n this example, the Person struct has two fields, `name` and `age`, and the `std::fmt::Display` trait is implemented for the struct. 
The `fmt()` method is called when a value of the Person type is formatted using the println! macro or other formatting macros. In this case, the `fmt()` method formats the name and age fields using the `write!()` `macro, which writes the formatted string to a buffer.

When the `println!` macro is called with alice and bob as arguments, the `fmt()` method is called for each value, 
and the resulting formatted strings are printed to the console. The output should look like this:


##### Custom formatting traits

Here's an example that defines a custom `Color` struct and implements the `std::fmt::Display` trait to customize how instances of the `Color` struct are formatted:

```rust
use std::fmt;

struct Color {
    red: u8,
    green: u8,
    blue: u8,
}

impl fmt::Display for Color {
    fn fmt(&self, f: &mut fmt::Formatter) -> fmt::Result {
        write!(f, "({}, {}, {})", self.red, self.green, self.blue)
    }
}

fn main() {
    let c = Color { red: 255, green: 165, blue: 0 };
    println!("The color is {}", c);
}
```

In this example, the `Color` struct has three fields, `red`, `green`, and `blue`, and the `std::fmt::Display` trait is implemented for the struct. The fmt() method is called when a value of the `Color` type is formatted using the println! macro or other formatting macros. In this case, the `fmt()` method formats the red, green, and blue fields using the `write!()` macro.

When the `println!` macro is called with c as an argument, the `fmt()` method is called for the `Color` value, and the resulting formatted string is printed to the console. The output should look like this:

Output:
```rust
The color is (255, 165, 0)
```

##### Alignment and padding

Here's an example that demonstrates how to use alignment and padding with the `println!` macro:

```rust
let x = 42;
let y = 3.14159265;
let s = "hello, world!";

println!("{:8}", x);                      // "      42"
println!("{:>8}", x);                     // "      42"
println!("{:<8}", x);                     // "42      "
println!("{:^8}", x);                     // "   42   "
println!("{:08}", x);                     // "00000042"
println!("{:+8}", x);                     // "     +42"
println
```

#### Different printing styles in rust

1. `println!()`: The println!() macro prints output to the console and automatically adds a newline character (\n) to the end of the output.

**Example:**
```rust
let name = "Alice";
let age = 30;
println!("Hello, {}! You are {} years old.", name, age);
```

Output:
```rust
Hello, Alice! You are 30 years old.
```

2. `print!()`: The print!() macro is similar to println!(), but it does not add a newline character to the end of the output.
**Example:**
```rust
let name = "Bob";
let age = 25;
print!("{} is {} years old. ", name, age);
print!("He is a software developer.");
```

**Output**
Bob is 25 years old. He is a software developer.


3. `format!()`: The format!() macro formats a string and returns the resulting string as a value. This is useful if you want to create a formatted string and then use it in a context where you cannot use the println!() or print!() macros, such as when returning a value from a function.
**Example:**
```rust
let name = "Charlie";
let age = 20;
let message = format!("{} is {} years old.", name, age);
println!("{}", message);
```

**Output**
```rust
Charlie is 20 years old.
```

4. `eprintln!()` and `eprint!()`: These macros work like println!() and print!(), but print to the standard error stream instead of standard output.

**Example:**
```rust
let error_message = "File not found";
eprintln!("Error: {}", error_message);
```

**Output**
```rust
Error: File not found
```

5. `dbg!()`: This macro is used for debugging purposes and prints the expression that is passed to it, along with the file name and line number where it was called.
**Example:**
```rust
let x = 42;
let y = 3.14;
let z = "Hello";
dbg!(x, y, z);
```

**Output**
```
[src/main.rs:4] x = 42
[src/main.rs:4] y = 3.14
[src/main.rs:4] z = "Hello"
```

#### Adding Comments

In Rust, there are two ways to add comments: single-line comments and multi-line comments.

1. Single-line comments: A single-line comment starts with // and continues to the end of the line. It can be used to add a short comment on a single line of code.
```rust
// This is a single-line comment
let x = 42; // You can also add a comment at the end of a line
```

2. Multi-line comments: A multi-line comment starts with `/*` and ends with `*/.` It can be used to add a longer comment that spans multiple lines of code.
```rust
/*
This is a multi-line comment.
It can span multiple lines of code.
*/
let x = 42;
```


Rust also supports Rustdoc-style comments, which are used to generate documentation for your code. These comments start with `///` or `//!,` and are explained in more detail in the Rust documentation.

---

### Variables

In Rust, a variable is a named memory location that can hold a value. The value stored in a variable can be of a particular type, and its type is determined at the time of declaration.

In Rust, variables are immutable by default, which means that their value cannot be changed after they have been assigned. 
To make a variable mutable, you need to use the `mut` keyword when declaring it.

> Here's an example of how to declare a variable in Rust:

```
let x: i32 = 42;
```

In this example, x is a variable of type i32 (a 32-bit signed integer), and it is initialized to the value 42. Since we didn't use the mut keyword, x is an immutable variable, which means that we cannot change its value later in the code.

If we want to make x mutable, we can use the mut keyword:

```rust
let mut x: i32 = 42;
x = 10; // This is allowed because x is now mutable
```


In this example, x is declared as a mutable variable using the mut keyword. We can then assign a new value to x later in the code.

Rust also supports shadowing, which is a way to re-declare a variable with the same name as an existing variable. When you shadow a variable, the new variable takes precedence over the previous one, and the old variable becomes inaccessible.

Here's an example of variable shadowing in Rust:

```rust
let x: i32 = 42;
let x: f64 = 3.14; // This shadows the previous variable x
```

In this example, we first declare x as a variable of type `i32`. We then declare a new variable with the same name `x`, but this time it's of type `f64`. This shadows the previous variable `x`, and we can no longer access its value or type.

##### Categories of types: scalar types and compound types. Each category includes several types that can be used to declare variables.

1. **Scalar types:** Scalar types represent a single value. Rust has four primary scalar types: integers, floating-point numbers, booleans, and characters.

* **Integers:** Integers are whole numbers. Rust supports signed and unsigned integers of various sizes, from 8 bits to 128 bits.

```
let a: i8 = -128; // signed 8-bit integer
let b: u16 = 65535; // unsigned 16-bit integer
let c: i32 = 42; // signed 32-bit integer
let d: u64 = 1000000; // unsigned 64-bit integer
```

* **Floating-point numbers:** Floating-point numbers are numbers with a decimal point. Rust supports f32 (single-precision) and f64 (double-precision) floating-point numbers.

```
let a: f32 = 3.14; // single-precision floating-point number
let b: f64 = 3.141592653589793238; // double-precision floating-point number
```

* **Booleans:** Booleans represent a value of either true or false.

```
let a: bool = true; // boolean with value true
let b: bool = false; // boolean with value false
```

* **Characters:** Characters represent a single Unicode scalar value, and are declared using single quotes.

```
let a: char = 'a'; // character 'a'
let b: char = '😀'; // character '😀' (a smiley face)

```

2. **Compound types:** Compound types are types that group multiple values into one type. Rust has two primary compound types: tuples and arrays.

* **Tuples:** Tuples are a fixed-length sequence of values of different types. You can access individual elements of a tuple using indexing, starting at 0.
```
let a: (i32, f64, char) = (42, 3.14, 'a'); // a tuple with three values
let b = a.0; // the first element of the tuple (42)
let c = a.1; // the second element of the tuple (3.14)
let d = a.2; // the third element of the tuple ('a')
```

* **Arrays:** Arrays are a fixed-length sequence of values of the same type. You can access individual elements of an array using indexing, starting at 0.
```
let a: [i32; 3] = [1, 2, 3]; // an array with three elements
let b = a[0]; // the first element of the array (1)
let c = a[1]; // the second element of the array (2)
let d = a[2]; // the third element of the array (3)
```
