# Systems

---

Systems are the logic processors that operate on entities with specific components. They define how entities behave based on their components. For instance, a `MovementSystem` might update the position of all entities with both `Position` and `Velocity` components every frame.

## Creating Systems

In Bevy, systems are functions that operate on entities with specific components. You can define systems using the `System` trait or as simple functions. Here's an example of a simple system that prints a message:

```rust
use bevy::prelude::*;

fn my_system() {
    println!("Hello, Bevy!");
}
```

In this example, `my_system` is a simple function that prints a message to the console. You can define more complex systems that interact with entities, components, and resources in your game.

## Adding Systems to the App

To add a system to your Bevy app, you can use the `add_systems` method on the `AppBuilder`. Here is an example of adding the `my_system` to the app:

```rust
fn main() {
    App::build()
        .add_systems(Update, my_system)
        .run();
}
```

In this example, the `my_system` function is added to the app using the `add_system` method. You can add multiple systems to the app by calling `add_systems` multiple times or by passing a tuple of systems instead of just a single system.

## System Execution Order

Bevy has a system scheduler that has different Game Phases that you can add systems to. The most common Game Phases are:
 * `First`: Systems added to this phase will run before any other systems.
 * `PreUpdate`: Systems added to this phase will run before the update phase.
 * `Update`: Systems added to this phase will run every frame.
 * `PostUpdate`: Systems added to this phase will run after the update phase.
 * `Last`: Systems added to this phase will run after all other systems.
 * `FixedPreUpdate`: Systems added to this phase will run on the fixed update rate, before the Fixed Update phase, which is useful for physics systems.
 * `FixedUpdate`: Systems added to this phase will run on the fixed update rate, which is useful for physics systems.
 * `FixedPostUpdate`: Systems added to this phase will run on the fixed update rate, after the Fixed Update phase, which is useful for physics systems.
 * `StartUp`: Systems added to this phase will run once at the start of the app.
 * `OnEnter(State)`: Systems added to this phase will run when entering a specific state.
 * `OnExit(State)`: Systems added to this phase will run when exiting a specific state.

Bevy will by default automatically try to run systems in parallel when possible. This means that the order in which systems are added does not necessarily determine the order in which they are executed. If you need to ensure a specific execution order, you can use the `before` and `after` methods to specify dependencies between systems.

## Run Conditions

You can specify run conditions for systems to control if they should run. Run conditions are closures that return a `bool` value. If the closure returns `true`, the system will run; otherwise, it will be skipped. Here's an example of a system with a run condition:

a common use case for run conditions are if certain key has been pressed. Bevy provides common conditions for you to use. Here is an example of a system that only runs if the `W` key is pressed:

```rust
use bevy::prelude::*;
use bevy::input::common_conditions::*;

fn my_system() {
    println!("Hello, Bevy!");
}

fn main() {
    App::build()
      .add_systems(Update, my_system.run_if(input_just_pressed(KeyCode::W)))
        .run();
}
```

In this example, the `my_system` function is added to the app with a run condition that checks if the `W` key has been pressed. If the condition is met, the system will run; otherwise, it will be skipped.

## System Queries

Queries are used to filter entities based on their components. Systems can define queries to select entities with specific component combinations, enabling targeted processing. For example, a system might query for entities with `Position` and `Velocity` components to update their movement.

Here's an example of a system that queries for entities with a `Position` component:

```rust
use bevy::prelude::*;

fn my_system(query: Query<&Position>) {
    for position in query.iter() {
        println!("Position: {:?}", position);
    }
}
```

In this example, the `my_system` function takes a `Query` of `Position` components as an argument. The system iterates over all entities with a `Position` component and prints their positions.

## Updating Components

Systems can update components on entities by using the `Commands` resource. The `Commands` resource allows you to spawn, despawn, or modify entities and their components. Here's an example of a system that updates the position of entities:

```rust
use bevy::prelude::*;

fn my_system(mut commands: Commands, query: Query<(Entity, &mut Position)>) {
    for (entity, mut position) in query.iter_mut() {
        position.x += 1.0;
        position.y += 1.0;
    }
}
```

In this example, the `my_system` function takes a `Commands` resource and a query of entities with `Position` components. The system updates the position of each entity by incrementing the `x` and `y` fields.

## Adding components to entities

Systems can add components to entities by using the `Commands` resource. The `Commands` resource allows you to spawn, despawn, or modify entities and their components. Here's an example of a system that adds a `Velocity` component to entities:

```rust
use bevy::prelude::*;

fn my_system(mut commands: Commands, query: Query<Entity>) {
    for entity in query.iter() {
        commands.entity(entity).insert(Velocity { x: 1.0, y: 1.0 });
    }
}
```

In this example, the `my_system` function takes a `Commands` resource and a query of entities. The system adds a `Velocity` component to each entity with an initial `x` and `y` value.

## Removing components from entities

Systems can remove components from entities by using the `Commands` resource. The `Commands` resource allows you to spawn, despawn, or modify entities and their components. Here's an example of a system that removes a `Velocity` component from entities:

```rust
use bevy::prelude::*;

fn my_system(mut commands: Commands, query: Query<(Entity, &Velocity)>) {
    for (entity, _) in query.iter() {
        commands.entity(entity).remove::<Velocity>();
    }
}
```

In this example, the `my_system` function takes a `Commands` resource and a query of entities with `Velocity` components. The system removes the `Velocity` component from each entity.

## Remove entities

Systems can remove entities by using the `Commands` resource. The `Commands` resource allows you to spawn, despawn, or modify entities and their components. Here's an example of a system that removes entities:

```rust
use bevy::prelude::*;

fn my_system(mut commands: Commands, query: Query<Entity>) {
    for entity in query.iter() {
        commands.entity(entity).despawn();
    }
}
```

In this example, the `my_system` function takes a `Commands` resource and a query of entities. The system despawns each entity, removing it from the game world.



