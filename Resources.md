# Resources

---

If you need to have data that is a `Singleton` you can use `Resources`.

## Defining a Resource
Resources are defined by creating a new Rust struct and deriving the `Resource` trait from Bevy. Here's an example of a simple `Score` resource:

```rust
use bevy::prelude::*;

#[derive(Resource)]
struct Score {
    value: i32,
}
```

In this example, we define a `Score` struct with a `value` field of type `i32`. By deriving the `Resource` trait, Bevy can automatically manage this resource within its ECS system.

## Accessing a Resource
Resources must first be added to the Bevy app using the `AppBuilder` method `insert_resource`. Here is an example of adding the `Score` resource to the app:

```rust
fn main() {
    App::build()
        .insert_resource(Score { value: 0 })
        .run();
}
```

or by defining a default value for the resource and using the `init_resource` method:

```rust
#[derive(Resource, Default)]
struct Score {
    value: i32,
}

fn main() {
    App::build()
        .init_resource::<Score>()
        .run();
}
```

Once a resource is added to the app, you can access it in your systems by adding a parameter to the system function with the resource type. Here's an example of a system that accesses the `Score` resource:

```rust
fn my_system(score: Res<Score>) {
    println!("Score: {}", score.value);
}
```

In this example, the `my_system` function takes a `Res<Score>` parameter, which allows it to access the `Score` resource. You can access the resource's fields and modify them as needed within the system.

## Modifying a Resource
Resources can be modified by using the `ResMut` type in system functions. Here's an example of a system that modifies the `Score` resource:

```rust
fn my_system(mut score: ResMut<Score>) {
    score.value += 10;
}
```

