# Input

---

Input in Bevy is handled by the `Input` plugin, which provides a way to interact with user input events such as keyboard, mouse, and touch events. The `Input` plugin is enabled by default in Bevy, so you don't need to do anything special to use it.

## Handling Input Events

To handle input events in Bevy, you can use the `Input` resource. The `Input` resource provides access to the current state of the input devices, such as the keyboard, mouse, and touch events. You can use the `Input` resource to check for input events and respond to them in your game.

Here's an example of a system that prints a message when the `W` key is pressed:

```rust
use bevy::prelude::*;

fn my_system(input: Res<ButtonInput<KeyCode>>) {
    if input.just_pressed(KeyCode::W) {
        println!("The 'W' key was just pressed!");
    }
}
```