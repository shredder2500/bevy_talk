# Bevy Setup

---

## Installing Bevy

Bevy is available as a set of Rust crates on [crates.io](https://crates.io/). To create a new Bevy project, add the bevy crate:

```shell
cargo add bevy
```

There are a bunch of optional configuration flags that you can enable to improve compile times in development. You can find them in the [Bevy Getting Started Page](https://bevyengine.org/learn/quick-start/getting-started/setup/#compile-with-performance-optimizations)

## Bevy Application

Now that we have the Bevy create installed, we now need to initialize a bevy Application. This is normally down in the `main.rs` file. Here is an example of how to initialize a Bevy application:

```rust
use bevy::prelude::*;

fn main() {
    App::build()
        .add_plugins(DefaultPlugins)
        .run();
}
```

This will create a new Bevy application with the default plugins enabled.

## Running the Application

To run the application, you can use the `cargo run` command:

```shell
cargo run
```

This will compile and run the Bevy application. You should see a window open with a blank screen.