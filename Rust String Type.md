2024-09-11 21:23

Status: #ownership #complete #very-long

Tags: [[RUST]] [[LEARNING]] [[CODING]]

---

Different from other data types the String type is great for exploring how the `HEAP` stores and cleans up data. 

```rust
let mut s = String::from("hello"); //Here we're making the string variable mutable while using the from method which makes it a String type.

s.push_str(", world!"); // .push_str appends a new string to the previous, making a combined string. Note that this does NOT need a new variable.

println!("{s}") 
```

### String Literals vs String

So, what’s the difference here? Why can `String` be mutated but literals cannot? The difference is in how these two types deal with memory.

String literals are <mark style="background: #FFB86CA6;">hard-coded</mark> into the binary, remaining there forever in the stack but are inconvenient due to the fact that they are immutable and are forever there, occupying memory.

Strings on the other hand aren't hard-coded into the binary but are mutable and able to be cleared by the heap. 

### String Type

When we make a value with the string type, it creates 2 tables: One that contains the pointer, the length and the capacity and the other that contains the index and the values. Look at this block:

```rust
let s1 = String::from("hello");
let s2 = s1;
```

This block states that `s1` is a String with the String data type and that `s2` copies `s1`. 
If `s2` had to copy the heap values too, it would've been a very big waste of memory if the data on the heap was huge.

When we do that `s1` becomes invalid since it `moved` into `s2`, thus not needing to free anything thus not decreasing performance.

If for some strange reason we want to make a deep copy of a variable, we'd use the `.clone()` method.

#### Difference

```rust
let x = 5;
let y = x;

println!("x = {x}, y = {y}");
```

This won't give an error since types such as integers that have a known size at compile time are stored entirely on the stack. Thus meaning that there's no reason to prevent `x` from being a valid value after we `copy` it to `y`.


```rust
let s1 = String::from("Hello");
let s2 = s1.clone();
```
### Drop Trait

```rust
fn main(){

    {
        let x: i32 = 20;
        
    }
    println!("{x}")

}
```

This gives an error since Rust <mark style="background: #FFB86CA6;">dropped</mark> the x variable as soon as it went out of scope.

```rust
fn main() {
    let s = String::from("hello");  // s comes into scope

    takes_ownership(s);    // s's value moves into the function...
                                    // ... and so is no longer valid here

    let x = 5;                      // x comes into scope

    makes_copy(x);                  // x would move into the function,
                                    // but i32 is Copy, so it's okay to still
                                    // use x afterward

} // Here, x goes out of scope, then s. But because s's value was moved, nothing
  // special happens.

fn takes_ownership(some_string: String) { // some_string comes into scope
    println!("{some_string}");
} // Here, some_string goes out of scope and `drop` is called. The backing
  // memory is freed.

fn makes_copy(some_integer: i32) { // some_integer comes into scope
    println!("{some_integer}");
} // Here, some_integer goes out of scope. Nothing special happens.
```


The ownership of a variable follows the same pattern every time: assigning a value to another variable <mark style="background: #FFF3A3A6;">moves it</mark>. When a variable that includes data on the `heap` goes out of scope, the value will be cleaned up by dropping it unless ownership of the data has been moved to another variable.



