# Player Jersey Customization

A Unity Shader Graph solution for applying a base jersey texture with independently customizable player name and number overlays.

**Author:** Gautam Dev

## Overview

Player Jersey Customization uses Unity Shader Graph, TextMeshPro, cameras, and RenderTextures to display a player name and number on a 3D jersey.

The base jersey texture remains unchanged. The name and number are rendered into separate transparent RenderTextures and composited over the jersey using the shader.

Each overlay has independent scale and position controls.

## Features

- Base jersey texture support.
- Separate player name and number overlays.
- Independent scale and position controls for each overlay.
- Alpha transparency to preserve the jersey texture beneath the overlays.
- Runtime text generation using TextMeshPro.
- Runtime updates through a C# customization script.
- MaterialPropertyBlock support for per-renderer customization.

## Requirements

- Unity with Shader Graph support.
- A compatible render pipeline, such as URP.
- TextMeshPro.
- A 3D character model with suitable UV coordinates.

## How It Works

The shader samples the base jersey texture using the mesh's UV coordinates.

The name and number are sampled as two additional textures. Each overlay has its own UV transformation, allowing it to be scaled and repositioned independently of the base texture and the other overlay.

The overlay UVs are transformed around a centered UV origin so scaling occurs around the center rather than the UV origin.

The alpha channel of each overlay determines its visibility. Transparent pixels reveal the jersey texture underneath, while opaque pixels display the name or number.

The shader blends the overlays with the base jersey texture to produce the final surface color.

## Setup

### 1. Set Up the Name Canvas and Camera

1. Create a Canvas and set its Render Mode to **Screen Space - Camera**.
2. Add a TextMeshPro UGUI text object for the player name.
3. Create a dedicated Unity Layer for the name Canvas and its text.
4. Create an orthographic camera for rendering the name.
5. Set the camera's Culling Mask to include only the name layer.
6. Assign the name camera to the Canvas's Render Camera field.
7. Set the camera's background to transparent (RGBA 0, 0, 0, 0).

### 2. Set Up the Number Canvas and Camera

Repeat the same process for the player number:

1. Create a separate Canvas with Render Mode set to **Screen Space - Camera**.
2. Add a TextMeshPro UGUI text object for the player number.
3. Create a dedicated Unity Layer for the number Canvas and its text.
4. Create a separate orthographic camera.
5. Set its Culling Mask to include only the number layer.
6. Assign the number camera to the Canvas's Render Camera field.
7. Set the camera's background to transparent (RGBA 0, 0, 0, 0).

### 3. Create the RenderTextures

Create two RenderTextures: one for the name and one for the number.

Suggested settings:

| Setting | Name RenderTexture | Number RenderTexture |
|---|---:|---:|
| Resolution | 1024 × 256 | 1024 × 1024 |
| Color format | ARGB32 | ARGB32 |
| Filter mode | Bilinear | Bilinear |
| Wrap mode | Clamp | Clamp |

Assign each RenderTexture to the Target Texture field of its corresponding camera. Use a format that preserves alpha transparency.

### 4. Create and Configure the Jersey Material

1. Create a material using the provided Jersey Shader Graph.
2. Assign the base jersey texture to the base texture property.
3. Assign the number RenderTexture to the number overlay property (`_Layer2`).
4. Assign the name RenderTexture to the name overlay property (`_Layer3`).
5. Adjust the position and scale properties for each overlay.

The Shader Graph properties used by the customization script must have the matching Reference names and be configured with **Per Material** scope.

| Shader property | Purpose |
|---|---|
| `_Layer2` | Number RenderTexture |
| `_Position` | Number position |
| `_Scale` | Number scale |
| `_Layer3` | Name RenderTexture |
| `_Layer3Position` | Name position |
| `_Layer3Scale` | Name scale |

### 5. Configure the Customization Script

Add the `PlayerJerseryCustomization` component to the character or another suitable GameObject.

Assign the following references in the Inspector:

- **Jersey Renderer:** The character renderer containing the jersey material.
- **Material Index:** The material slot that uses the jersey Shader Graph.
- **Number Text / Name Text:** The corresponding TextMeshPro UGUI objects.
- **Number Camera / Name Camera:** The cameras used to render each text layer.
- **Number RT / Name RT:** The corresponding RenderTextures.

Set the player name and number, then adjust the position and scale values to fit the character's UV layout.

The script detects changes to the name, number, position, and scale values during Play Mode and applies the updates automatically.

## Runtime Customization

The customization script exposes the player name and number as public strings.

For example:

```csharp
playerCustomization.playerName = "RONALDO";
playerCustomization.playerNumber = "7";
```

When these values change during Play Mode, the script regenerates the corresponding text RenderTexture and updates the jersey.

Position and scale changes update the shader properties without regenerating the text textures.

The script uses a `MaterialPropertyBlock` to apply the customization to the selected renderer material slot without creating a separate material instance for each player.

## Notes and Troubleshooting

- Ensure the character mesh has suitable UV coordinates for the jersey design.
- Use transparent backgrounds for both text cameras.
- Ensure each camera's Culling Mask includes its corresponding Canvas layer.
- Do not use **Screen Space - Overlay** for canvases that must be rendered by these cameras.
- Ensure both RenderTextures use a format that supports alpha.
- Confirm that the Shader Graph Reference names match the names listed above.
- Set the relevant Shader Graph properties to **Per Material** scope when using the supplied `MaterialPropertyBlock` script.
- Confirm that the script's Material Index points to the renderer slot using the jersey shader.
- Adjust the camera framing, Canvas layout, text alignment, and font size to suit the chosen RenderTexture dimensions.

## Credits

**Developed by Gautam Dev**

Built with Unity Shader Graph and TextMeshPro.
