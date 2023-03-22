# If statements

You cannot use an expression return (the return without `return` and `;`) in an if statement.
If you do this, the compiler assumes you're trying to do an `let x = if ...`.

```
// Works
let x = if amount > 40 {
    amount * 2
} else {
    aomunt * 3
}
```

```
// Works
if amount > 40 {
    return amount * 2;
} else {
    return amount * 3;
}
```

```
// Doesn't compile
if amount > 40 {
    amount * 2
} else {
    amount * 3
}
```
