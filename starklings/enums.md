# Enums

Empty enums:

```
enum Message {
    Quit: (),
    Echo: (),
    Move: (),
    ChangeColor: ()
}
```

Enum with value

```
enum Message {
    Quit: (),
    Echo: felt252,
    Move: (),
    ChangeColor()
}
```

Enum with struct

```
enum Message {
    Quit: (),
    Echo: felt252,
    Move: Point,
    ChangeColor()
}

struct Point {
    x: u8,
    y: u8
}
```

Enum with tuple

```
enum Message {
    Quit: (),
    Echo: felt252,
    Move: (),
    ChangeColor(u8, u8, u8)
}
```
