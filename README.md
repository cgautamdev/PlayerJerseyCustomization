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

## Shader Setup

1. Create or open the `CustomJersey_ShaderGraph` Shader Graph.
2. Add the properties listed above to the Blackboard.
3. Set the property reference names exactly as shown in the table. The C# script uses these reference names to access the material properties.
4. Use the jersey base, AO, smoothness, normal, and metallic textures for the corresponding Lit shader inputs.
5. The number and name textures are handled as separate overlay branches in the graph.
6. Each overlay has its own UV scale and position controls, so the player name and number can be adjusted independently.

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

## Troubleshooting

- **Name or number does not appear:** Check that the correct texture is assigned to the matching Shader Graph property.
- **Name or number is in the wrong place:** Adjust its corresponding position and scale vectors independently.
- **Material properties are reported as missing:** Confirm that the jersey Renderer is using the correct material in the configured material slot, and that the Shader Graph property reference names match the table exactly.
- **Changes do not appear:** Confirm that the script references the intended Renderer, material slot, TMP objects, cameras, and RenderTextures.

---

Author: Gautam Dev
