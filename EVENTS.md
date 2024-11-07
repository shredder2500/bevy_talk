# Events

Events in Bevy are a way to send messages between systems. You can use events to communicate between systems without having to pass data directly. This can be useful for decoupling systems and making your code more modular.

## Defining an Event

Events in Bevy are defined by creating a new Rust struct and deriving the `Event` trait from Bevy. Here's an example of a simple `PlayerDied` event:

```rust
use bevy::prelude::*;

#[derive(Event)]
struct PlayerDied;
```

In this example, we define a `PlayerDied` struct that represents an event where the player has died. By deriving the `Event` trait, Bevy can automatically manage this event within its ECS system.

## Sending an Event

To send an event in Bevy, you can use the `EventWriter` resource. Here's an example of sending a `PlayerDied` event:

```rust
fn my_system(mut player_died_events: EventWriter<PlayerDied>) {
    player_died_events.send(PlayerDied);
}
```

In this example, the `my_system` function takes a `EventWriter<PlayerDied>` parameter, which allows it to send `PlayerDied` events. You can send events from any system in your app.

## Receiving an Event

To receive an event in Bevy, you can use the `EventReader` resource. Here's an example of receiving a `PlayerDied` event:

```rust

fn my_system(player_died_events: EventReader<PlayerDied>) {
    for _ in player_died_events.iter() {
        println!("Player died!");
    }
}
```