<p align="center">
  <img src="https://cdn.rawgit.com/dragostis/pest/e0de86ef8a85b83f66da6f338258fb7114c489f9/pest-logo.svg"/>
</p>
# pest. Elegant, efficient grammars
[![Build Status](https://travis-ci.org/dragostis/pest.svg?branch=master)]
(https://travis-ci.org/dragostis/pest)
[![Coverage Status]
(https://coveralls.io/repos/github/dragostis/pest/badge.svg?branch=master)]
(https://coveralls.io/github/dragostis/pest?branch=master)
[![Cargo Crate](http://meritbadge.herokuapp.com/pest)]
(https://crates.io/crates/pest)

pest is a [PEG](https://en.wikipedia.org/wiki/Parsing_expression_grammar) parser
generator with *simplicity* and *speed* in mind.

## Elegant

pest uses PEG syntax to enable expressive grammar creation.

```rust
impl_rdp! {
    grammar! {
        exp = { paren ~ exp | [""] }
        paren = { ["("] ~ exp ~ [")"] }
    }
}

let mut parser = Rdp::new(StringInput::new("(()((())())()")));

assert!(parser.exp());
assert!(parser.end());
```

## Fast

pest generates a fast parser at compile time through the use of macros, without
forcing you to use nightly. Yes, it works on **stable** (1.9.0+).

Here are some preliminary tests for your enjoyment.

| Parser generator | Time to parse 272.5 KB of JSON |
|------------------|--------------------------------|
| ANTRL 4          | 153,000 μs (+/- 15,000)        |
| Bison + Flex     | 8,761.9 μs (+/- 697)           |
| **pest**         | 3,178.9 μs (+/- 40.6)          |

## Features

* simple PEG grammar
* smart error reporting with `atomic` and `silent` rules
* no generation step (one-step compilation)
* fast macro-generated recursive descent parser
* runs on stable Rust
* elegant functional-style `Token` processing

## Roadmap

* [Packrat parsing](issues/7)
* [parsing parallelization](issues/25)
