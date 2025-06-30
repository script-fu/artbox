---
type: docs
url: "hub/feature-test/folder/Dynamic-Velocity-Compression"
---

# Objective

Improve the quality of dynamics driven by velocity input.

## Design Revisions

{{< cards >}}
  {{< card link="#velocity-mapping" title="Velocity Mapping" subtitle="Logarithmic compression for natural motion" icon="lightning-bolt" >}}
{{< /cards >}}

---

<div class="feature-section" id="velocity-mapping">

## Velocity Mapping

**Current State**: Velocity is clamped to a limit.

**Issue**: The users input motion velocity is clipped at an arbitrary value. Strokes lack a realistic sense of motion.

**Solution**: Add a compress_velocity function for logarithmic velocity normalization. Lower speeds are more sensitive, faster motions are compressed rather than clamped, this gives a more natural feel. Also removes a subtle filtering artifact.

**Technical Details**: Uses a log function, no discernible slowdown on a _fast_ pc.

**Visual Comparison**:

**Without Feature**: Left side is a slow to fast stroke, right side has inverted velocity mapping
![without-feature](/images/diagrams/brush-velocity-compression-without-feature.webp)

**With Feature**: Left side is a slow to fast stroke, right side has inverted velocity mapping
![with-feature](/images/diagrams/brush-velocity-compression-with-feature.webp)

**Implementation Details**:

- **Logarithmic Velocity Compression**: Introduces a new compression function that maps raw velocities to a compressed range using a logarithmic scale. Enhances sensitivity for low velocities, allowing for finer control during slow movements. Prevents compressed velocities from saturating too quickly at high raw velocities, ensuring a smooth transition across the velocity spectrum.

- **Improved Smoothing Mechanism**: Utilizes a consistent exponential smoothing factor in the velocity calculations. Provides stable and smooth transitions by reducing abrupt changes in velocity. Ensures the smoothed velocity is correctly maintained for accurate computations in subsequent events.

- **Optimizations and Refactoring**: Adds precomputed constants for logarithmic calculations to optimize performance. Refactors code to correctly update `buffer->last_coords.velocity` after assignments to prevent unintended overwrites. Includes detailed comments explaining the purpose of constants like `V_MAX`, `k`, and `V_THRESHOLD`, aiding future maintenance and readability.

**Benefits**: These enhancements result in more responsive and natural tool dynamics within GIMP's drawing tools, offering users improved control and a better overall experience when interacting with dynamic brushes and other velocity-dependent features.

</div>

---
