---
type: docs
url: "hub/feature-test/folder/Paintbrush-Smooth-Stroke"
---

# Paintbrush Smooth Stroke

To provide a more intuitive and comprehensive `Smooth Stroke` GUI and extend its behavior to cover stroke direction and pressure. It should feel natural to use and be easily customizable.

## Design Revisions

{{< cards >}}
  {{< card link="#rename-existing-sliders" title="Rename Existing Sliders" subtitle="More intuitive Quality and Weight labels" icon="tag" >}}
  {{< card link="#add-new-sliders" title="Add New Sliders" subtitle="Pressure and Direction smoothing controls" icon="adjustments" >}}
  {{< card link="#change-smoothing-algorithm" title="Change Smoothing Algorithm" subtitle="Simpler averaging method" icon="beaker" >}}
{{< /cards >}}

---

<div class="feature-section" id="rename-existing-sliders">

## Rename Existing Sliders

**Current State**: `Quality` and `Weight` are the two available sliders.

**Issue**: "Quality" and "Weight" are not intuitive for users to relate to on-canvas effects.

**Solution**: `Quality` is renamed to `Depth`, as it controls the number of historical points used in smoothing. `Weight` is renamed to `Position`, as it now controls the blend between raw stroke positions and smoothed positions.

</div>

<div class="feature-section" id="add-new-sliders">

## Add New Sliders

**Current State**: New Feature.

**Issue**: There is no smoothing for pressure or direction.

**Solution**: Added `Pressure` and `Direction` sliders to control smoothing. Setting `0` for the `Direction` slider deactivates that aspect.

**Implementation**: Introduced new smoothing options for brush strokes:
- **Position Smoothing**: Controls the smoothing of brush positions.
- **Pressure Smoothing**: Smooths pressure changes over the stroke.
- **Direction Smoothing**: Smooths stroke direction for a more stable flow.

</div>

<div class="feature-section" id="change-smoothing-algorithm">

## Change Smoothing Algorithm

**Current State**: Gaussian-based averaging.

**Issue**: The previous Gaussian-based smoothing approach involved more complex math. It was found that a simpler averaging method was sufficient for the desired effects.

**Solution**: The new algorithm uses a simpler core averaging method, making it easier to extend to position, pressure, and direction smoothing. New data structures and testing functions have been introduced for validation.

**Advanced Details**: The algorithm uses velocity and history based weighting, with simple averaging and linear blending for stroke attributes from raw to smoothed:
- Faster strokes give more weight to recent points for increased responsiveness.
- Slower strokes distribute weight evenly, leading to smoother transitions.
- The algorithm calculates weighted averages for brush coordinates (position, pressure, direction) and blends them with the current stroke, resulting in smoother, more controlled movements.

**Testing Framework**: Functions simulate different stroke profiles: `STROKE_LINEAR`, `STROKE_SLOW_TO_FAST`, `STROKE_FAST_TO_SLOW`, and `STROKE_SLOW_IN_SLOW_OUT`. A testing framework outputs detailed tables showing how smoothing affects stroke parameters (position, pressure, direction). This framework helps validate and refine the smoothing algorithm with data such as `average_x`, `average_y`, and `average_pressure`.

</div>

---

### **Benefits**

These updates significantly improve brush stroke handling in Artbox. The new smoothing options give artists greater control over brush behavior, providing more responsive fast strokes and smoother slow strokes. The updated algorithm and new testing tools simplify the process of refining stroke behavior, making the painting experience more predictable and enjoyable. Entirely new types of brush strokes can be created by using the `Pressure` and `Direction` sliders.

