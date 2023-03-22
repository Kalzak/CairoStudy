# Options

Options are slightly different in Cairo.

You need to import the option trait to be able to use options.

```
use option::OptionTrait;
```

To use the `Some()` and `None` than with Rust. See the following:

```
if condition == true {
    return Option::Some(10_usize);
} else {
    return Option::None(());
}
```

The `None` needs to have an empty value inside it. Both of them need to use `Option` rather than using `Some` or `None` directly.
