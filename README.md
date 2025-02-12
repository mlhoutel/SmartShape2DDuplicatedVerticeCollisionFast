# SmartShape2D duplicated vertice collision fast

## Description

This project demonstrates an issue when using the **SmartShape2D** plugin with **Rapier2D** in Godot 4.3. The issue occurs when associating a `CollisionPolygon2D` with `SS2D_Shape` and setting the collision generation method to **Fast**.

Each time the collision shape is updated (e.g., clicking the refresh button in the editor), Rapier2D throws errors.

## Tested Versions

- **Godot:** v4.3-stable
- **SmartShape2D Plugin:** v3.2.0
- **Rapier2D:** v0.8.8

## Issue

When linking a `CollisionPolygon2D` to an `SS2D_Shape` and enabling fast collision generation, the `bake_collision` function causes errors in Rapier2D:

### Cause

This happens when an **invalid polygon** (overlapping edges or duplicate vertices) is provided to Rapier, as the generated points include a **duplicate first and last vertex**, leading to invalid geometry.

## Steps to Reproduce

1. Create a new physics collider object.
2. Add a `CollisionPolygon2D` to it.
3. Set the **Build Mode** of `CollisionPolygon2D` to **Solids**.
4. Add an `SS2D_Shape` to the scene.
5. Link the `CollisionPolygon2D` in the **Collision Polygon Node Path** of `SS2D_Shape`.
6. Set the **Collision Generation Method** to **Fast**.
7. Click the **Refresh** button in the editor to update the collision shape.
8. Observe errors from Rapier2D in the console.

## Expected Behavior

The `SS2D_Shape` should generate a valid collision shape without causing errors in Rapier2D.
