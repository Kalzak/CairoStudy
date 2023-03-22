# Primitive types

### Short strings

These are strings whose lengths are at most 31 characters.
Therefore these can fit inside a single field element, so they are actually felts, not a real string.
Single quotes are used with short strings.

According to `primitive_types2.cairo` it seems they can be neither? Not sure how that works.

### Refs

In Rust you can use `ref` on both mutable and immutable references.
In Cairo you can only use it on mutable variables?
It seems that `ref` is the syntactic alternative to Rust's `&`.
In Rust you can only use `ref` when declaring function parameters, or in a match statement.
In Cairo it seems you can use `ref` for function arguments (or maybe just wherever).

**QUESTION**: Why do variables need to be `mut` for `ref` to work in Cairo? This isn't the same in Rust.

### Extracting values out of tuples

```
let tuple = ('abc', 123);
let (alpha, num) = tuple;
```

### Integers, felts and casting

You have the integer types: `u8` `u16`, `u32`, `usize`, `u64`, `u128` and `u256`.
Overflow checks for these types are done automatically.

You can cast an integer type into a felt with `into()`.

```
let x = 12;
let x_felt = x.into()
```

You can cast a felt to an integer with `try_into()` but you need to unwrap the result because option returned.

```
let x: felt252 = 255;
let x_int: u8 = x.try_into().unwrap();
```
