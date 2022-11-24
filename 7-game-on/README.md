# Passing Criteria:

## Add a New Feature: (F)ocus Cube

While the Player is holding the `F`-Key:
- `A` and `D` lets the player move left and right.
  - relative to his own axes
- `W` and `S` lets the player move up and down.
  - relative to his own axes

Otherwise:
- `A` and `D` lets the player move left and right.
  - relative to his own axes
- `W` and `S` lets the player forward and backward.
  - relative to his own axes
- Moving the Mouse on the X-Axis lets the player look left and right.
- Moving the Mouse on the Y-Axis lets the player look up and down.

## Add a Hint of Physics:
- Add Gravity, which makes the Player fall towards the Plane
- Stop the Players Fall when he is on height of the Plane
  - Add a little Offset, so it doesn't look like the Player's a Mouse
- Allow the Player to jump when he presses `Space`
- Disable Gravity while the player is holding the `F`-Key
  - The player can "pull himself on" while focusing the Cube

# Excellent Criteria:

## Add a new Object:
- Add a `PyramidMesh` that looks like a Pyramid.
  - Use a proper UV-Layout with the `Wall`-Texture
  - The edges will most likely not be seamless.
- Add a `MeshRenderer` that renders said `PyramidMesh`.
- Make that Pyramid orbit around the Cube in the Center.
- Make that Pyramid also turn around its own axis