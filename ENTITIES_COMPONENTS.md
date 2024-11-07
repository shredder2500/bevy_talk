# Entities and Components

---

In Bevy, entities are the fundamental building blocks of the game world. They represent unique objects such as players, enemies, or items. Entities are lightweight identifiers that do not contain any data or behavior themselves. Instead, entities are composed of components, which are data containers that hold attributes related to entities.

## Components

Components are the data containers that define the attributes and behaviors of entities. For example, a `Position` component might store the coordinates of an entity, while a `Health` component could represent its hit points. Components are lightweight and can be easily added, removed, or modified on entities, allowing for dynamic behaviors and interactions.

### Creating Components

To create a new component in Bevy, you define a Rust struct and derive the `Component` trait from Bevy. Here's an example of a simple `Position` component:

```rust
use bevy::prelude::*;

#[derive(Component)]
struct Position {
    x: f32,
    y: f32,
}
```

In this example, we define a `Position` struct with `x` and `y` fields of type `f32`. By deriving the `Component` trait, Bevy can automatically manage this component within its ECS system.

### Spawn Entities with Components

Once you have defined components, you can create entities with specific components using Bevy's entity spawning system. Here's an example of spawning an entity with a `Position` and `Rotation` component:

```rust
use bevy::prelude::*;

fn spawn_entity(commands: &mut Commands) {
    commands.spawn((
        Position { x: 0.0, y: 0.0 },
        Rotation { radians: 0.0 },
      ));
}
```

