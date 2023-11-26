---
title: API Days 2023 Rust
revealOptions:
  transition: "fade"
---

[<img src="imgs/rust-logo.png" alt="rust logo" style="height: 200px">](https://www.rust-lang.org/)

<br>

API Days Paris - Zacaria Chtatar - December 2023

https://havesome-rust-api-day.surge.sh

---

## Forget TypeScript

## Choose Rust to build

## Robust, Fast and Cheap APIs

---

<!--
## Typescript

- Dev UX

* Makes you forget that utimately it executes Javascript
* Makes you forget that it generates far more Javascript than you think
* Extensive type system which can block progression even if execution path is right
* Needs ecosystem support in order to not be a pain working with libraries

---

### My Opinion

- JSDoc is more than enough to reach DX without the tradeoffs
- *** -->

---

# "Why" : History & context

timeline

---

**Discuss why there's a need to rethink the current approach to building APIs. ????**

---

## TS pain points

Address the pain points with current technologies (like TypeScript).

## JSDoc is enough to get max value without overhead

---

Emphasize the importance of reliability, speed, and cost-effectiveness in API development.

=> Now what

---

# "What"

---

## Introducing Rust

_Fast, Reliable, Productive: pick three._

---

## Fast

---

<img src="imgs/comparison.png" style="height: 450px">

note:

The stakes of software are increasingly complex.

- space
- time
- functionality
- concurrency
- security

space: memory footprint
time: execution speed, startup time
functionality: quantity of functionality, you need to refactor
security: quantity of bugs possible increase, and each failure or bug can impact millions

---

## Reliable

---

<img src="imgs/billion-dollar-mistake.jpg" style="height: 250px">

---

Borrow checker by default guarantees :

- No memory leaks
- No use-after-free
- No dangling pointers
- Runtime type system

---

What's wrong with this code ?

```js
function readFile(path) {
  return fs.readFileSync(path);
}
```

---

```rust
fn read_file(path: &str) -> Result<String, io::Error> {
    fs::read_to_string(path)
}
```

```rust
fn read_file(path: &str) -> String {
    fs::read_to_string(path).unwrap()
}
```

Make it clear of what could go wrong

---

2016 : Do you remember the [left-pad drama](https://qz.com/646467/how-one-programmer-broke-the-internet-by-deleting-a-tiny-piece-of-code) ?

no package un publish

---

- Linux project
- Microsoft project

---

## Cheap

- CPU and RAM consumption

---

## Sexy

today Rust is the most loved language according SO for 8 years

When I go to JS meetups, lots of people speaking of Rust

So people are interested

---

Why does Rust makes you build apps that "work good" ?

note:

What does working good mean ?

- predictable : it always does what you expect it to do
- recovers from errors
- secure
- scales

---

- Compiled
- No GC
- No manual memory management Borrow checker
- developed in Rust

=> There is no blackbox between you and the machine

note:

developed in rust so you will always be able to know what happens inside

---

# Embeded tools

- compiler errors
- fmt
- clippy
- tests
- documentation

note:

tested documentation

---

## Compiler

- hight and low level : compilation with zero cost abstraction : example

note:

Being high and low level at the same time levels up the dev's skills
You learn how to think like a computer while writing expressive code

**It's like some fundamental problem has been solved**

---

## Default tooling

- cargo

- gouvernance

  Introduce Rust as a solution to these challenges.
  Briefly mention what Rust is and its rising popularity in the software development world.

---

# "How"

---

Slide: Rust in Action
Dive into how Rust addresses the pain points you've identified.
Discuss Rust's features like ownership, concurrency, and performance, and how they translate to better API development.

---

Slide: Rust vs. TypeScript
Compare Rust with TypeScript, focusing on practical differences in API development scenarios.

---

# "Benefits"

---

Slide: The Rust Advantage
Highlight the key benefits of using Rust – reliability, efficiency, and cost savings.

---

Slide: Success Stories
Share case studies or examples where Rust has been successfully used to build robust APIs.

- projects
- Discord
- Cloudflare
- Github

---

# "When and Where"

---

t3 chart

---

Process to get started: POV dev

- Books : official, google, lets get rusty
- cheatsheet : lime
- Advent of code
- YT channels
  - Noboilerplate
  - Code to the Moon
- server framework : axum

---

Process to get started: POV manager

- find dev interested in Rust : there are a lot
- give opportunity with simple projects
  - build small CLI
  - lambdas
  - microservice
  - network app
  - devops tools

---

Show archi to go for

- REST : [axum](https://github.com/graphql-rust/juniper)
- GraphQl : [juniper](https://github.com/graphql-rust/juniper)
- ***

Slide: Getting Started with Rust
Offer guidance on when and where to start incorporating Rust into API development.
Provide resources for learning Rust and integrating it into existing projects.

---

# Conclude with "Future Vision"

Slide: The Future of API Development
Paint a picture of the future where Rust plays a key role in API development.
Inspire your audience to be part of this future.

---

# Q&A

Slide: Open for Questions
Encourage audience engagement and address any queries or concerns.

---

## Conclusion

recap

Say again the main idea

---

### Thank you

<img src="imgs/crab2.png" style="height: 30vh">
