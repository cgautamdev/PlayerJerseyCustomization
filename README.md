# Custom Jersey Shader Graph

A Unity Shader Graph setup for customizing a jersey with separate player-name and player-number textures. The shader also exposes the jersey's base and surface maps, along with independent scale and position controls for the name and number.

## Shader Graph Properties

The Blackboard contains the following properties:

| Property | Type | Purpose |
|---|---|---|
| `Jersey_Base` | Texture2D | Main jersey/base texture |
| `Jersey_AO` | Texture2D | Ambient occlusion map |
| `Jersey_Smoothness` | Texture2D | Smoothness map |
| `Jersey_Normal` | Texture2D | Normal map |
| `Jersey_Metallic` | Texture2D | Metallic map |
| `JerseyNumberTexture` | Texture2D | Player-number texture |
| `JerseyNameTexture` | Texture2D | Player-name texture |
| `JerseyNumberScale` | Vector2 | Scale of the number overlay |
| `JerseyNumberPosition` | Vector2 | Position of the number overlay |
| `JerseyNameScale` | Vector2 | Scale of the name overlay |
| `JerseyNamePosition` | Vector2 | Position of the name overlay |

## How It Works

The shader uses the object's UV map as the input for the Sample Texture 2D nodes that read the jersey textures. The sampled jersey texture is then connected to the Fragment output.

A centered UV is used for the two text overlays. Each overlay has its own Sample Texture 2D node and independent scale and position controls:

- The player-name overlay uses the name texture, name scale, and name position.
- The player-number overlay uses the number texture, number scale, and number position.

The two overlays are first blended with the base jersey texture using Lerp nodes. The overlay results are then blended together using the combined alpha values from the sampled textures.

## How to Set Up and Use

### 1. Set Up the Name Camera

Create a camera for the player-name text. Set the camera to **Orthographic** and use it with a **Screen Space - Camera** canvas containing only the name text.

Create a separate layer for the name text, then set the camera's Culling Mask to include only that layer.

### 2. Set Up the Number Camera

Repeat the same setup for the player number:

- Create a separate camera and set it to **Orthographic**.
- Use a **Screen Space - Camera** canvas containing only the number text.
- Place the number text on its own layer.
- Set the camera's Culling Mask to include only that layer.

### 3. Create and Assign the RenderTextures

Create two RenderTextures: one for the name and one for the number. Choose a color format that supports alpha.

Assign each RenderTexture as the output texture for its corresponding camera.

### 4. Create and Configure the Material

Create a material using the shader and assign the name and number RenderTextures to their corresponding texture properties.

Adjust the scale and position controls for the name and number to place both overlays correctly on the jersey.

## Material Setup

1. Create a material using `CustomJersey_ShaderGraph`.
2. Assign the jersey's base, AO, smoothness, normal, and metallic maps.
3. Assign the player-number texture to `JerseyNumberTexture`.
4. Assign the player-name texture to `JerseyNameTexture`.
5. Adjust `JerseyNumberScale`, `JerseyNumberPosition`, `JerseyNameScale`, and `JerseyNamePosition` to set the size and placement of both overlays.

## Suggested RenderTexture Settings

Create separate RenderTextures for the player name and player number.

| Setting | Suggested value |
|---|---|
| Name texture size | 1024 × 256 |
| Number texture size | 1024 × 1024 |
| Color format | `B8G8R8A8_UNORM` |
| Filter Mode | Bilinear |
| Wrap Mode | Clamp |

Choose texture dimensions that suit the jersey UV layout and the amount of text being displayed.
