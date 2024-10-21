---
type: docs
---

# Objective

To provide a more intuitive and comprehensive `Smooth Stroke` GUI and extend its behavior to cover stroke direction and pressure. It should feel natural to use and be easily customizable.

## Design Revisions

| **Revision**  | **Current Design**  | **Issues**  | **Changes** |
|---------------|---------------------|-------------|-------------|
| **1. Rename Existing Sliders** | `Quality` and `Weight` are the two available sliders | "Quality" and "Weight" are not intuitive for users to relate to on-canvas effects. | `Quality` is renamed to `Depth`, as it controls the number of historical points used in smoothing. `Weight` is renamed to `Position`, as it now controls the blend between raw stroke positions and smoothed positions. |
| **2. Add Sliders** | New Feature | There is no smoothing for pressure or direction. | Added `Pressure` and `Direction` sliders to control smoothing. Setting `0` for the `Direction` slider deactivates that aspect. |
| **3. Change the Smoothing Algorithm** | Gaussian-based averaging | The previous Gaussian-based smoothing approach involved more complex math. It was found that a simpler averaging method was sufficient for the desired effects. | The new algorithm uses a simpler core averaging method, making it easier to extend to position, pressure, and direction smoothing. New data structures and testing functions have been introduced for validation. |

## MR Description

This update replaces the previous brush stroke smoothing and introduces new configuration options for brush behavior.

### Changes

1. **Brush Smoothing Functionality**:
   - Introduced new smoothing options for brush strokes:
     - **Position Smoothing**: Controls the smoothing of brush positions.
     - **Pressure Smoothing**: Smooths pressure changes over the stroke.
     - **Direction Smoothing**: Smooths stroke direction for a more stable flow.

2. **Stroke Simulation and Testing**:
   - Functions simulate different stroke profiles: `STROKE_LINEAR`, `STROKE_SLOW_TO_FAST`, `STROKE_FAST_TO_SLOW`, and `STROKE_SLOW_IN_SLOW_OUT`.
   - A testing framework outputs detailed tables showing how smoothing affects stroke parameters (position, pressure, direction).
   - This framework helps validate and refine the smoothing algorithm with data such as `average_x`, `average_y`, and `average_pressure`.

3. **Revised Smoothing Algorithm**:
   - The algorithm uses velocity and history based weighting, with simple averaging and linear blending for stroke attributes from raw to smoothed:
     - Faster strokes give more weight to recent points for increased responsiveness.
     - Slower strokes distribute weight evenly, leading to smoother transitions.
   - The algorithm calculates weighted averages for brush coordinates (position, pressure, direction) and blends them with the current stroke, resulting in smoother, more controlled movements.

### Benefit

These updates significantly improve brush stroke handling in Artbox. The new smoothing options give artists greater control over brush behavior, providing more responsive fast strokes and smoother slow strokes. The updated algorithm and new testing tools simplify the process of refining stroke behavior, making the painting experience more predictable and enjoyable. Entirely new types of brush strokes can be created by using the `Pressure` and `Direction` sliders.

