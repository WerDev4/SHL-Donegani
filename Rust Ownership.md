2024-09-11 20:18

Status: #new #ownership

Tags: [[RUST]] [[LEARNING]] [[CODING]]

---

Ownership is Rust's most unique feature. It makes rust safe without a garbage collector which would make it slow.  

### Ownership Rules

- `Each value in Rust has an owner.`
- `There can only be one owner at a time.`
- `When the owner goes out of scope, the value will be dropped`

    ```rust

    {                      // s is not valid here, it’s not yet declared
        let s = "hello";   // s is valid from this point forward
                           // stuff here
    }                     
                           // Not in stack anymore
 ```

- `When s comes into scope, it is valid.`
- `It remains valid until it goes out of scope.`

