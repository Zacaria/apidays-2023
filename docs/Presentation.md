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

----

**Discuss why there's a need to rethink the current approach to building APIs. ????**

----

## TS pain points

- types disappear at runtime
- does not save from dealing with JS
- adds complexity
- no semver

Address the pain points with current technologies (like TypeScript).

** JSDoc is enough to get max value without overhead **

----

## New stakes, new needs

Emphasize the importance of reliability, speed, and cost-effectiveness in API development.

<!-- The stakes of software are increasingly complex. -->

- stability
- memory footprint
- computation
- functionality
- security

space: memory footprint
time: execution speed, startup time
functionality: quantity of functionality, you need to refactor
security: quantity of bugs possible increase, and each failure or bug can impact millions

----

# "What"

---

## Introducing Rust

_Fast, Reliable, Productive: pick three._

---

## Fast

----

<img src="imgs/comparison.png" style="height: 450px">

----

## Reliable

----

<img src="imgs/billion-dollar-mistake.jpg" style="height: 250px">

----

Borrow checker by default guarantees :

- No memory leaks
- No use-after-free
- No dangling pointers
- Runtime type system

----

What's wrong with this code ?

```ts
function readFile(path: string): string {
  return fs.readFileSync(path);
}
```

----

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

----

2016 : Do you remember the [left-pad drama](https://qz.com/646467/how-one-programmer-broke-the-internet-by-deleting-a-tiny-piece-of-code) ?

no package un publish

----

- Linux project
- [Microsoft](https://msrc.microsoft.com/blog/2019/07/a-proactive-approach-to-more-secure-code/) project

---

## Cheap

- CPU and RAM consumption
- Less bugs
- [Firecracker](https://firecracker-microvm.github.io/)

---

## Sexy

----

Rust is the most loved language according [SO](https://survey.stackoverflow.co/2023/#section-admired-and-desired-programming-scripting-and-markup-languages) for 8 years

When I go to JS meetups, lots of people speaking of Rust

People are interested

note:

From my perspective that a good recruitment argument

As a more difficult than average technology
By recruiting Rust developers you get higher than average devs
Rust teachings can be used even outside of Rust projects

---

### Why does Rust apps "work well" ?

note:

What does working well mean ?

- predictable : it always does what you expect it to do
- recovers from errors
- secure
- scales

----

- Compiled
- No GC
- No manual memory management : Ownership & Borrow checker
- developed in Rust

=> There is no blackbox between you and the machine

note:

developed in rust so you will always be able to know what happens inside

---

## Compiler

- error messages and hints
- hight and low level : compilation with zero cost abstraction : example

note:

Being high and low level at the same time levels up the dev's skills
You learn how to think like a computer while writing expressive code

**It's like some fundamental problem has been solved**

---

## Tools

- cargo test : IT, UT
- cargo fmt
- cargo bench
- clippy
- bacon
- rust-analyzer

----

#### Cargo doc stays up to date

```rust [|6-7|]
/// Formats the sum of two numbers as a string.
///
/// # Examples
///
/// ```
/// let result = mycrate::sum_as_string(5, 10);
/// assert_eq!(result, "15");
/// ```
pub fn sum_as_string(a: i32, b: i32) -> String { (a + b).to_string() }
```

`cargo doc --open`

note:

coverage
executed during tests
keeps examples up to date

---

## AI

When I started, Rust documentation was designed for C++ devs

- ChatGPT
- Copilot / Codeium
- [lets get rusty](https://www.youtube.com/@letsgetrusty/)

note:

Helps with discovery

---

## Governance

Rust Project

[Rust Foundation](https://foundation.rust-lang.org/)

Release process

---

# "How"

----

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

## Success Stories

Share case studies or examples where Rust has been successfully used to build robust APIs.

projects :
- [Discord](https://discord.com/blog/why-discord-is-switching-from-go-to-rust)
- Cloudflare
- Github
- [others](https://github.com/omarabid/rust-companies)

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
