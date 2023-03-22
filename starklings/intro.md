# Intro

You can have a Cairo contract compile with just an empty `main`:

```
fn main() {}
```

You can define types for function args as follows:

```
fn add(a: felt252, b: felt252) -> felt252 {
    a + b
}
```
