# Bevy Plugins

---

Bevy plugins allow modular functionality to be added to your game project. Plugins can be pulled in as dependencies or exist in your code base to help organize and extend your game's features. This guide will cover the basics of Bevy plugins and how to use them effectively.

## How Plugins Work

Bevy plugins are functions that have the plugin trait `Plugin`. They can be added to the Bevy app using the `add_plugins` method. Plugins can be used to add systems, resources, components, or other features to your game.

Here is an example of a simple plugin that adds a system to the Bevy app:

```rust
use bevy::prelude::*;

struct MyPlugin;

impl Plugin for MyPlugin {
    fn build(&self, app: &mut AppBuilder) {
        app.add_systems(my_system);
    }
}
```

In this example, `MyPlugin` is a struct that implements the `Plugin` trait. The `build` method is called when the plugin is added to the app, and it can be used to add systems, resources, or other features to the app.

## Adding Plugins

To add a plugin to your Bevy app, you can use the `add_plugins` method on the `AppBuilder`. Here is an example of adding the `MyPlugin` from the previous example to the app:

```rust
fn main() {
    App::build()
        .add_plugins(DefaultPlugins)
        .add_plugins(MyPlugin)
        .run();
}
```

In this example, the `MyPlugin` is added to the app using the `add_plugins` method. You can add multiple plugins to the app by calling `add_plugins` multiple times or by passing a tuple of plugins instead of just a single plugin.