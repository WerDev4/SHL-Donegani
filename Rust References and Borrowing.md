2024-09-12 08:52

Status: #new #easy #long #ownership 

Tags: [[RUST]] [[LEARNING]] [[CODING]]

---

```rust
fn main() {
    let s1 = String::from("hello");

    let len = calculate_length(&s1);

    println!("The length of '{s1}' is {len}.");
}

fn calculate_length(s: &String) -> usize {
    s.len()
}
```

Here we can make `s1` still valid even after we use it in the `len` variable. That's because we don't code `calculate_length(s1)` which would've given the ownership of `s1` to the function thus making the variable not valid anymore.

![[Reference.svg]]

```rust
let s1 = String::from("hello");
let len = calculate_length(&s1);
```

The code block above shows how to make a reference to another variable, without moving it nor taking ownership. Even tho `&s1` creates a reference to `s1`, `s1`
does not own it thus will not be dropped after it's used.

* To make a reference add `randfunc(&var)`

## Changing A Reference
###### P.S: We can't

```rust
fn main() {
    let s = String::from("hello");

    change(&s);
}

fn change(some_string: &String) {
    some_string.push_str(", world");
}
```

This won't work because just like yo mom, references are immutable. 

To work it has to be like this:

```rust
fn main() {
    let mut s = String::from("hello");

    change(&mut s);
}

fn change(some_string: &mut String) {
    some_string.push_str(", world");
}
```

We have to add `mut` after mention the reference tag.

Trying to borrow a reference more than 1 time gives error.

