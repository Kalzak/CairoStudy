# Variables

The default type for integers seems to be `felt252`

Even though memory is immutable in StarkNet, we can still have `mutable` variables.
Under the hood this operates very similarly to reference rebinding in 0.X versions for Cairo

If you want to assign a different type to the same variable, you can't use `mut` because it's a different type.
But you can use shadowing instead, see how number becomes `u8` to `felt252` and back to `u8`

```
use debug::PrintTrait;

fn main() {
    let number = 1_u8;
    number.print();
    {
        let number: felt252 = 3;
        number.print();
    }
    number.print();
}

// Prints 1 then 3 then 1
```

Constants don't get compiler help to determine their type, you must always specify their type

```
const NUMBER: felt252 = 3;
const SMALL_NUMBER: u8 = 3_u8;
```
