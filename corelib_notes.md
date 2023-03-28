# Corelib notes

Notes based on [this](https://github.com/starkware-libs/cairo/tree/bc1ebcb8236603baa2b1f25bb04148a00aac0984/corelib/src) commit.

### array.cairo

Arrays have the following functions:

- `new()`
- `append()`
- `pop_front()`
- `get()`
- `at()`
- `len()`
- `is_empty()`
- `span()`

They also implement a `Span` which seems to be a read-only thing?
Not sure why it has `pop_front` though, I assume that would remove an element.

### box.cairo

Introduces a box trait and implementation, allowing for the functions:

- `new()`: Places some value in a `Box<T>`
- `unbox()`: Removed some value from a box

Is this some kind of alternative to the `Option`, `Some` and `None`?

### clone.cairo

Just defines a function `clone`, which accepts some `@` of a variables and then returns that dereferenced value.

Would that be a real clone? By looking at that code I imagine it would return the same data from the same memory right?

### debug.cairo

Defines a bunch of function for printing values out, useful for debugging.

Some example usage:

```
use debug::PrintTrait;

1.print();

(1 == 2).print();

get_caller_address().print();

let mut arr = ArrayTrait::new();
arr.append('1234567890123456789012345678901');
arr.append('Sca');
arr.append('SomeVeryLongMessage');
arr.print();
```

They only have one print function for `felt252` so every other type is converted into `felt252` and then printed.
The actual print function is defined as `extern fn print(message: Array<felt252>) nopanic;` and must be somewhere else.
They convert everything into a felt array and then print it.

### dict.cairo

Defines the `Felt252DictTrait` trait with four functions:

- `new()`
- `insert()`
- `get()`
- `squash()`

There is also a `Felt252DictDestruct` trait with the function `destruct()`.

### ec.cairo

Defines elliptic curve functions:

- `ec_point_try_new()`: Attempts to create a new point given an `x` and `y`, returns `Option` type
- `ec_point_new()`: Creates a new point gives an `x` and `y`
- `ec_point_from_x()`: Converts some `x` into a point
- `ec_point_non_zero()`: Converts some point to a `NonZeroEcPoint` type
- `ec_state_finalize()`: Finalizes some elliptic curve state and returns result
- `ec_mul()`: Returns the result of two points multiplied together
- `add()`: Returns the result of one point added with another
- `add_eq()`: Assigns the first `ref` argument to the result of point1 + point2
- `sub()`: Returns the result of one point subtracted by another
- `sub_eq()`: Assigns the first `ref` argument to the result of point1 - point2

### ecdsa.cairo

ECDSA signature checking logic, only has one function:

`check_ecdsa_signature()`, which accepts the following args:

- `message_hash`
- `public_key`
- `signature_r`
- `signature_s`

Will return a bool. False if not a valid signature, true if a valid signature

### gas.cairo

Uses the `extern` function declaration thing. Does this for three functions:

- `withdraw_gas()`
- `withdraw_gas_all()`
- `get_builtin_costs()`

### hash.cairo

A library that looks to be build on top of the `perdersen` low level hash function

Defines a bunch of functions for hashing booleans, all integer types, contract addresses, and tuple sizes up to 4

### integer.cairo

Defines all integer types and their functions. Here are the types:

- `u128`
- `u8`
- `u16`
- `u32`
- `u64`
- `u256`
- `u128`
- `u128`
- `u128`
- `u128`
- `u128`

Here are the functions:

- `uXXX_try_from_felt252()`
- `uXXX_to_felt252()`
- `uXXX_overflowing_add()`
- `uXXX_overflowing_sub()`
- `uXXX_wrapping_add()`
- `uXXX_wide_mul()`
- `uXXX_sqrt()`
- `uXXX_overflowing_mul()`
- `uXXX_checked_add()`
- `add()` (for the `+` operator)
- `add_eq()` (for the `+=` operator)
- `uXXX_checked_sub()`
- `sub()` (for the `-` operator)
- `sub_eq()` (for the `-=` operator)
- `uXXX_checked_mul()`
- `mul()` (for the `*` operator)
- `mul_eq()` (for the `*=` operator)
- `uXXX_try_as_non_zero()`
- `uXXX_u128_safe_divmod()`
- `div()` (for the `/` operator)
- `div_eq()` (for the `/=` operator)
- `rem()` (for the `%` operator)
- `rem_eq()` (for the `%=` operator)
- `uXXX_lt()`
- `uXXX_eq()`
- `uXXX_le()`
- `eq()` (for the `==` operator)
- `ne()` (for the `!=` operator)
- `le()` (for the `<=` operator)
- `ge()` (for the `>=` operator)
- `lt()` (for the `<` operator)
- `gt()` (for the `>` operator)
- `bitand()` (for the `&` operator)
- `bitxor()` (for the `^` operator)
- `bitor()` (for the `|` operator)
- `uXXX_is_zero()`
- `into()` (part of the `UXXXIntoFelt252` implementation/trait)

Note that `u256` still consists of a `high` and `low` value, just like with 0.x versions of Cairo.

### internal.cairo

Just declares `revoke_ap_tracking()` which I guess is a way to prevent the function from being accessed externally.
Not sure what the "ap" stands for though.

### lib.cairo

Lib is where everything should end up. So pretty much every other file mentioned here gets `use`'d from here.

It also defines some `bool` and `felt252` functions.

The `bool` function definitions are to hook the functions to the operators for `bool` types (`^`, `&`, `!`, `|`, `==`, `!=`). Also a function to covern `bool` to `felt252`: `bool_to_felt252`.

A similar thing is done for the `felt252` type. Not going to go through them but pretty much the same, plus div, mul, neg, equality checks etc.

Also defines the `PanicResult` enum here, along with defining the `assert` function.

### nullable.cairo

Defines the enum `FromNullableResult`, where you can have a `Null` entrie of a `NotNull` entry which is a `Box<T>`

### option.cairo

Defines the `Option<T>` enum and trait. Right now options are implemented into the language, not builtin.

This file contains the implementation for options.

An option can be `Some` of a given `T` type, or `None` which is `()`.

Functions:

- `expect()`: Panic with error if `None`, we expect `Some`
- `unwrap()`: Pretty much the same as above, but a generic panic rather than custom message
- `is_some()`: True if value is `Some`, otherwise false for `None`
- `is_none()`: True if value is `None`, otherwise false for `Some`

### poseidon.cairo

iirc this is some fancy zkcircuit hashing stuff that happens to be better for zero knowledge stuff? not 100% sure.

It defines the function `hades_permutation` which accets three `felt252`'s and returns three `felt252`s

Not really sure about this one, but here is a paper that explains it I guess: [https://eprint.iacr.org/2019/1107.pdf]()

### result.cairo

Defines the `Result` enum which can be `Ok` or `Err`.

Supports the following functions:

- `expect()`
- `unwrap()`
- `expect_err()`
- `unwrap_err()`
- `is_ok()`
- `is_err()`

### serde.cairo

Seems like some logic where you can "serialize" or "deserialize" a bunch of types

Not sure how this would be used or why though.

### starknet.cairo

This `use`'s a bunch of StarkNet related functionality and brings it into Cairo.

Here are some of them:

- `storage_access`
- `syscalls`
- `contract_address`
- `class_hash`
- `info`

Also implements a `SyscallResult` type with the only functionality being `unwrap_syscall()`

### test.cairo

A big file here. All it really does is test the implementanions in all the other files listed here.

So in terms of learning Cairo stuff it won't prove as useful. Going to skip over this.

### testing.cairo

Very small, only one line. Defines the extern function `get_available_gas`. Not sure why this is for testing only though.

I thought gas related stuff was part of normal execution? Maybe this is testing-specific stuff somehow?

### traits.cairo

Defines all the traits needed that will act as operators. (add, eq, sub, div, mod, etc...)

Pretty sure this gets used by all the other type implementations.

Also defines some one like `try_into()` and `destruct()` 

### zeroable.cairo

Defines a `Zeroable<T>` trait with the functions:

- `zero()`
- `is_zero()`
- `is_non_zero()`

This can apply to `felt252` values.
