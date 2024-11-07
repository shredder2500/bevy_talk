# Game State

---

Bevy allows you to define game states to manage different parts of your game. Game states are useful for separating different game modes, screens, or levels. By using game states, you can control which systems are active and which resources are available at any given time.

## Creating a Game State

To create a game state in Bevy, you define a new enum that implements the `States` trait. Here's an example of a simple game state:

```rust
use bevy::prelude::*;

#[derive(States, Debug, Clone, PartialEq, Eq, Hash)]
enum MyAppState {
    LoadingScreen,
    MainMenu,
    InGame,
}
```

In this example, we define a new enum `MyAppState` that represents different states of our game. Each variant of the enum represents a different game state, such as `LoadingScreen`, `MainMenu`, and `InGame`.

## Adding and initializing Game States

There are really two ways to add and initialize game states in Bevy. The first way is to add the states to the `AppBilder` using the `init_state` method. This method requires you to have set a default value for the enum.
Here is an example of adding the `MyAppState` enum to the app:

```rust
#[derive(States, Default, Debug, Clone, PartialEq, Eq, Hash)]
enum MyAppState {
  #[default]
  Paused,
  Running,
}

fn main() {
    App::build()
      .init_state::<MyAppState>()
        .run();
}
```

The second way is to add the states to the `AppBuilder` using the `insert_state` method. This method you will pass in the initial state you want to start with.

```rust
fn main() {
    App::build()
      .insert_state(MyAppState::Paused)
        .run();
}
```

## Using Game States to Control Systems

Once you have defined your game states, you can use them to control which systems are active at any given time. You can use the run conditions to specify which systems should run based on the current game state. Here's an example of a system that only runs when the game state is `InGame`:

```rust

fn main() {
    App::build()
        .add_systems(Update, my_system.run_if(in_state(MyAppState::InGame)))
        .run();
}
```

In this example, the `my_system` function is only run when the game state is `InGame`. You can use the `run_if` method to specify a run condition for the system based on the current game state.

You can also use the `OnEnter` and `OnExit` scheduling phases to run systems when entering or exiting a specific game state. Here's an example of a system that runs when entering the `InGame` state:

```rust

fn main() {
    App::build()
        .add_systems(OnEnter(MyAppState::InGame), my_system)
        .run();
}
```

In this example, the `my_system` function is run when the game state transitions to `InGame`. You can use the `OnExit` scheduling phase to run systems when exiting a specific game state.

## Changing Game States

You can change the game state at any time by using the `State` resource. The `State` resource allows you to set the current game state and transition between different states. Here's an example of changing the game state to `InGame`:

```rust
fn my_system(mut state: ResMut<State<MyAppState>>) {
    state.set(MyAppState::InGame);
}
```

