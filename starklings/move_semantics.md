# Move semantics

Pretty similar to rust apparently. It's not all the same but most concepts are similar.

### Passing mutable references for functions

```
fn main() {
    let mut value: felt252 = 1;
    change_value(ref value);
}

fn change_value(ref value: felt252) {
    value = 2;
}
```
### Passing mutables directly for functions

```
use array::ArrayTrait;

fn main() {
    // This leaves arr0 useless because moved
    let mut arr0 = ArrayTrait::new();

    let mut arr1 = fill_arr(arr0);
}

fn fill_arr(mut rar: Array<felt252>) -> Array<felt252> {
    arr.append(22);
    arr.append(44);
    arr.append(66);

    arr
}
```

### Snapshots and desnapping

Basically Cairo's approach to references and referencing.

The snapshot operator is `@` and the desnap is `*`

Here is an example

```
#[derive(Drop)]
struct Number {
    value: u32, 
}

fn main() {
    let mut number = Number { value: 1111111_u32 };
    get_value(@number);
    set_value(number);
}

fn get_value(number: @Number) -> u32 {
    *number.value
}

fn set_value(mut number: Number) {
    let value = 2222222_u32;
    number = Number { value };
}
```
