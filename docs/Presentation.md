---
title: API Days 2023 Rust
revealOptions:
  transition: "fade"
---

[<img src="imgs/rust-logo.png" alt="rust logo" style="height: 200px">](https://www.rust-lang.org/)

<br>

API Days Paris - Zacaria Chtatar - December 2023

https://havesome-rust-api-day.surge.sh

note:

Started dev and JS 10 years ago
And I love it
I love the fact that you can move quickly
The fact that you can use it everywhere
And that's the richest ecosystem ever

---

## Forget TypeScript

## Choose Rust to build

## Robust, Fast and Cheap APIs

note:

But today I'm going to suggest you to

Forget Typescript

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

----

Big brains decided to extract Chrome's JS VM to run JavaScript outside the browser

With this they created JS modules systems

Suddenly, it became really to reuse and build upon JS code.

The abstraction was so powerfull that it created the FullStack developers.

But the fullstack Java, dotNet statically typed developers

Did not like the powerful JS yet dangerous JavaScript.

The feeling of safety was no more when wrote JS.

----

So TypeScript came as a superset. Bringing types, checks and refactor capabilities.

The greed, we can all be guilty of, can even let us build a complete typed sidesystem around our functionalities.

Costing time and effort just to please the compiler

Unfortunately, what TS brings fades just after the compilation.

Types, classes, interfaces are gone.

At 4am when problems occur, it's JS that we have to deal with.

----

NodeJs & NPM

- modules
- boom of easy to reuse code
- fullstack JS. Easy to start with, hard to master
- fullstack from backend guys don't want to learn JS

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

## Stability

----

<img src="imgs/billion-dollar-mistake.jpg" style="height: 250px">

note:

When a value is unexpectedly null or undefined
That's an unvalid state
As a system programing language, Rust makes it easy to make invalid state unrepresentable
----

- compiled
- no GC
- memory management enforced by the compiler
- zero cost high level functions
- Bonus : devs level up


note:

- compiled : so it produces a specific output for each architecture
- no GC : memory is managed via a deterministic system called Borrow checker
- no manual memory management by default: it's enforced by the compiler
- Developers do the memory management by themselves, but now are guided by the rules of the compiler
- zero cost high level functions like map or filter are compiled to the same output as imperative loops
- As a side effect, the high level languages devs get closer to the machine and get better at writing correct code

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

no package unpublish

note:

cargo does not allow unpublishing
Instead it allows flagging packages and version to not be downloaded as new dependency

----

Linux: [Le Kernel](https://linux.developpez.com/actu/337316/Rust-for-Linux-est-officiellement-fusionne-le-support-initial-de-Rust-for-Linux-fournit-l-infrastructure-de-base-et-une-integration-elementaire/)

<img src="imgs/linus-logo.webp" style="height: 250px">

- 2/3 of vunerabilities come from memory management <!-- .element: class="fragment" data-fragment-index="1" -->
- Kernel is in C and Assembly <!-- .element: class="fragment" data-fragment-index="2" -->
- Linus Torvalds : ❌ C++ ❌ <!-- .element: class="fragment" data-fragment-index="3" -->
- attract young devs <!-- .element: class="fragment" data-fragment-index="4" -->

note:

<!-- - Linux project
- [Microsoft](https://msrc.microsoft.com/blog/2019/07/a-proactive-approach-to-more-secure-code/) project -->

---

## Fast

----

<img src="imgs/comparison.png" style="height: 450px">

note:

[Energy efficiency accross programing languages](https://greenlab.di.uminho.pt/wp-content/uploads/2017/10/sleFinal.pdf)

Energy measured using a framework (Computer Language Benchmarks Game) designed for running testing and comparing solutions to problems

And Intel's Running Average Power Limit (RAPL) tool which can measure energy consumption of an executed program.

----

#### Github: [Code Search index](https://github.blog/2023-02-06-the-technology-behind-githubs-new-code-search/)

<img src="imgs/github.png" style="background-color: whitesmoke; height: 150px">


45 million repos to index : <!-- .element: class="fragment" data-fragment-index="1" -->

- several months with Elasticsearch <!-- .element: class="fragment" data-fragment-index="2" -->
- 18h in Rust <!-- .element: class="fragment" data-fragment-index="3" -->

----

#### Clouflare: [HTTP proxy](https://blog.cloudflare.com/how-we-built-pingora-the-proxy-that-connects-cloudflare-to-the-internet/)

<img src="imgs/cloudflare-logo.png" style="background-color: whitesmoke; height: 150px">

- nginx not fast enough 🤯 <!-- .element: class="fragment" data-fragment-index="1" -->
- hard to customize in C <!-- .element: class="fragment" data-fragment-index="2" -->
- allows to share connections between threads <!-- .element: class="fragment" data-fragment-index="3" -->

= 160x less connections to the origins <!-- .element: class="fragment" data-fragment-index="4" -->

= 434 years less handshakes per day <!-- .element: class="fragment" data-fragment-index="5" -->

----

#### Discord: [Message read service](https://discord.com/blog/why-discord-is-switching-from-go-to-rust)

<img src="imgs/discord-logo.png" style="background-color: red; height: 70px">


- Cache of a few billion entries <!-- .element: class="fragment" data-fragment-index="1" -->
- Every connection, message sent and read... <!-- .element: class="fragment" data-fragment-index="2" -->
- latences toutes les 2 minutes en Go à cause du GC <!-- .element: class="fragment" data-fragment-index="3" -->

<img src="imgs/discord_rex.png" style="height: 250px"> <!-- .element: class="fragment" data-fragment-index="4" -->

note:

Thanks to no GC
Instead of stopping the world to clean unused memory
Every variable is cleaned at a precise moment
For the devs, that's the purpose of ownership

---

## Cheap

- CPU and RAM consumption

- Less maintenance with less bugs

----

### AWS Lambda

- [Firecracker](https://firecracker-microvm.github.io/)

---

## Sexy

----

Rust is the most admired language according [SO](https://survey.stackoverflow.co/2023/#section-admired-and-desired-programming-scripting-and-markup-languages) for 8 years

When I go to JS meetups, lots of people speaking of Rust

People are interested

note:

From my perspective that a good recruitment argument

As a more difficult than average technology
By recruiting Rust developers you get higher than average devs
Rust teachings can be used even outside of Rust projects

----

### It's a challenge

- It take 3 to 6 months to become productive

- It's not **that** hard

- Documentation was oriented towards C/C++ senior devs

note:

[Study](https://blog.rust-lang.org/2020/12/16/rust-survey-2020.html)

As a manager recruiting someone who successfully wen through the process of learning Rust

It's a safe bet in the technical aspect

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

Helps with functions discovery and paradigm

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

# Downsides ?

- Project moves a bit slower

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
