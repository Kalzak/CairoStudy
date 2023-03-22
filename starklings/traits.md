# Traits

A trait is a collection of methods.
Data types can implement traits. The methods making up the trait are defined for the data type.
EG: `felt` implements the `Into` trait, allowing `1.into()`

An example of traits is in the `structs.md` markdown file.

You can have trait that applies to multiples types. Here `AnimalTrait` applies to `Cat` and `Cow` through `CatImpl` and `CowImpl`.

```
#[derive(Copy, Drop)]
struct Cat {
    noise: felt252,
}

#[derive(Copy, Drop)]
struct Cow {
    noise: felt252,
}

trait AnimalTrait<T> {
    fn new() -> T;
    fn make_noise(self: T) -> felt252;
}

impl CatImpl of AnimalTrait::<Cat> {
    fn new() -> Cat {
        Cat { noise: 'meow' }
    }
    fn make_noise(self: Cat) -> felt252 {
        self.noise
    }
}

impl CowImpl of AnimalTrait::<Cow> {
    fn new() -> Cow {
        Cow {noise: 'moo' }
    }
    fn make_noise(self: Cow) -> felt252 {
        self.noise
    }
}
```

The general structure seems to be:

1) Have your struct or datatype with `<name>`
2) Define your traits for the struct (just name, inputs, outputs) as `trait <name>Trait {...}`
3) Implement the trait logic in `impl <name>TraitImpl of <name>Trait {...}`
