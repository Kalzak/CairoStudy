# Structs

Defining a struct:

```
struct ColorStruct {
    red: felt252,
    green: felt252,
    blue: felt252
}
```

Creating a struct:

```
let green = ColorStruct {
    red: 0,
    green: 255,
    blue: 0
}
```

Accessing struct elements:

```
let green = ColorStruct {
    red: 0,
    green: 255,
    blue: 0
}

let structgreen = green.red;
```

## Adding logic to structs

```
use array::ArrayTrait;
#[derive(Copy, Drop)] // Not sure what drop does
struct Numbers {
    a: felt252,
    b: felt252
}

trait NumbersTrait {
    fn new(a: felt252, b: felt252) -> Numbers;
    fn add(ref self: Numbers) -> felt252;
    fn increase_a(ref self: Numbers, amount_to_increase: felt252);
}

impl NumbersImpl of NumbersTrait {
    fn new(a: felt252, b: felt252) -> Numbers {
        Numbers {a, b}
    }

    fn add(ref self: Numbers) -> felt252 {
        self.a + self.b
    }

    fn increase_a(ref self: Numbers, amount_to_increase: felt256) {
        self.a = self.a + amount_to_increase;
    }
}
```
