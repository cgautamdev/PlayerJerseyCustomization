# Custom Jersey Shader Graph

## How It Works

The shader uses the object's UV map as the starting point for sampling the jersey textures. The sampled jersey texture is then connected to the Fragment output.

A centered UV is also used to position and scale the two text overlays: the player name and the player number.

Each overlay has its own set of inputs:

- Name texture, scale, and position
- Number texture, scale, and position

The two overlays are first blended with the base jersey texture using Lerp nodes. The overlay results are then blended together using the combined alpha from the sampled textures.

## How to Set Up and Use

### 1. Set Up the Name Camera

- Create a camera with **Screen Space - Camera** rendering for the name text.
- Set the camera to **Orthographic**.
- Place only the name text on a separate layer.
- Set the camera's Culling Mask to include only that layer.

### 2. Set Up the Number Camera

Repeat the same setup for the player number:

- Create a separate camera with **Screen Space - Camera** rendering.
- Set it to **Orthographic**.
- Place only the number text on its own layer.
- Set the camera's Culling Mask to include only that layer.

### 3. Create the RenderTextures

- Create two RenderTextures: one for the name and one for the number.
- Choose a color format that supports alpha.
- Assign each RenderTexture as the output texture for its corresponding camera.

### 4. Create and Configure the Material

- Create a material that uses the Custom Jersey Shader Graph.
- Assign the name and number RenderTextures to their corresponding texture properties.
- Adjust the scale and position controls for the name and number until both overlays are placed correctly on the jersey.
