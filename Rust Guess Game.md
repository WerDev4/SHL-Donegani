2024-09-11 18:38

Status: #new #game 

Tags: [[RUST]] [[LEARNING]] [[CODING]]

---

Yesterday i've learned how to do a simple "guess the number game" in rust. It is very easy, python level easy. 

```rust


//Purpose is for reading input (input() in python)
use std::io;

//rand Crate, used for making random numbers
use rand::Rng;

//Used for comparrison
use std::cmp::Ordering;

//main function of rust
fn main() {

    println!("Guess the numba!"); //used for giving an output into terminal

    let secret_number = rand::thread_rng().gen_range(1..=100); //makes a secret number using Rand Crate

    //println!("The secret number is: {secret_number}");
    loop{ //makes loops until broken
    
    println!("Please input your guess.");

    let mut guess = String::new(); //makes new mutable variable

    io::stdin() //reads line and assigns the value tu 'guess'
        .read_line(&mut guess)
        .expect("Failed to read line"); //error handling
    
    let guess: u32 = match guess.trim().parse() { //adjusts the 'guess' variable to be compatible with an integer, trim is used for trimming the variable from any useless info ex: \n or \r\n.
        Ok(num) => num,
        Err(_) => continue,
    };

    println!("You guessed: {}", guess); 

    match guess.cmp(&secret_number) { //uses the Ordering Crate to compare the Guess variable to the secret number. 
        Ordering::Less => println!("Too small!"),
        Ordering::Greater => println!("Too big!"),
        Ordering::Equal => {
            println!("You win!");
            break;
        }
    }
    }
}
```




