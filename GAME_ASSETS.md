# Game Assets

---

Game assets are the resources used in your game, such as images, sounds, and fonts. Bevy provides a simple way to load and manage these assets using the `AssetServer` resource.

## Loading Assets

To load an asset in Bevy, you can use the `load` method on the `AssetServer`. Here is an example of loading an image asset:

```rust
use bevy::prelude::*;

fn load_assets(asset_server: Res<AssetServer>) {
    let texture_handle = asset_server.load("texture.png");
}
```

In this example, we use the `load` method on the `AssetServer` to load an image asset named `texture.png`. The `load` method returns a `Handle` to the asset, which can be used to access the asset in your game.

## Using Assets

Once you have loaded an asset, you can use it in your game by adding it to the appropriate resources. For example, you can add a texture asset to the `Assets<Texture>` resource like this:

```rust
fn add_texture_to_resources(
    mut commands: Commands,
    asset_server: Res<AssetServer>,
    mut textures: ResMut<Assets<Texture>>,
) {
    let texture_handle = asset_server.load("texture.png");
    commands.spawn(SpriteBundle {
        texture: texture_handle,
        ..Default::default()
    });
}
```
