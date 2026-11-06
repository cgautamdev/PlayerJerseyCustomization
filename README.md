# Custom Jersey Shader Graph

A Unity Shader Graph setup for customizing a jersey with separate player-name and player-number textures. The shader also exposes the jersey's base and surface maps, along with independent scale and position controls for the name and number.

## Shader Graph Properties

The Blackboard contains these properties:

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

## Material Setup

1. Create a material from `CustomJersey_ShaderGraph`.
2. Assign the jersey's base, AO, smoothness, normal, and metallic maps in the material.
3. Assign the player-number texture to `JerseyNumberTexture`.
4. Assign the player-name texture to `JerseyNameTexture`.
5. Adjust `JerseyNumberScale`, `JerseyNumberPosition`, `JerseyNameScale`, and `JerseyNamePosition` to place and size the text on the jersey.

## C# Script Configuration

The `PlayerJerseryCustomization` script is designed to work with the shader properties above.

Assign the following references in the Inspector:

- The jersey Renderer.
- The material slot that uses the Custom Jersey Shader Graph material.
- The TMP text objects used to generate the player name and number textures.
- The cameras and RenderTextures used for the name and number.

The script's public fields can be edited in the Inspector while the game is running. Changes to the name, number, scale, or position are detected and applied to the jersey.

## Suggested RenderTexture Settings

Use separate RenderTextures for the player name and number.

| Setting | Suggested value |
|---|---|
| Name texture size | 1024 × 256 |
| Number texture size | 1024 × 1024 |
| Color format | B8G8R8A8_UNORM |
| Filter Mode | Bilinear |
| Wrap Mode | Clamp |

Choose texture dimensions that suit the jersey UV layout and the amount of text being displayed.
---

