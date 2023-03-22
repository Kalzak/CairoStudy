# Arrays

You can use an import array methods by importing the `array::ArrayTrait` trait.
Arrays are append only. You can only add elemnts to the end of an array.
You cannot remove or modify element in an array (kind of)
This is because StarkNet memory is immutable.

Arrays must be mutable

You can create an array as follows:

```
// Need this trait imported
use array::ArrayTrait;

let mut array = ArrayTrait::new();
```

You can append to arrays as follows:

```
// Need this trait imported
use array::ArrayTrait;

let mut array = ArrayTrait::new();
a.append(1);
a.append(2);
a.append(3);
```

You can get the length of an array as follows:

```
// Need this trait imported
use array::ArrayTrait;

let mut array = ArrayTrait::new();
array.append(1);
array.append(2);
array.append(3);

let length = array.len();
```

You can go through elements with pops. 
When you pop it doesn't clear the memory, it just moves up the starting location for the pointer.

```
// Note that you'll need the option trait

let value = array.pop_front().unwrap();
```

You can also use the `at` trait which seems to autounwrap which could be bad

```
let value = *array.at(0_usize);;`
```

You have the `get` trait which returns an option which is better

```
let value = 0;
if array.get(0_usize).is_some() {
    value = array.get(0_usize).unwrap();
}
```
