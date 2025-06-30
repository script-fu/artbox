---
type: docs
url: "hub/feature-test/folder/Dynamic-Brush-Spacing"
---

# Objective

Improve the quality of the brush spacing with respect to velocity.

## Design Revisions

{{< cards >}}
  {{< card link="#remove-spacing-limits" title="Remove Spacing Limits" subtitle="Respect Paint Tool slider settings" icon="view-grid" >}}
{{< /cards >}}

---

<div class="feature-section" id="remove-spacing-limits">

## Remove Spacing Limits

**Current State**: Spacing is set to 200% for fast.

**Issue**: Spacing does not respect the Paint Tool slider settings.

**Solution**: Spacing respects the slider values.

**Background**: This feature branch was a proposed solution to https://gitlab.gnome.org/GNOME/gimp/-/issues/1863

**Visual Comparison**:

**Without Feature**: Top is a slow stroke, middle line fast, lower is slow to fast.
![without-feature](/images/diagrams/brush-velocity-without-feature.webp)

**With Feature**: Top is a slow stroke, middle line fast, lower is slow to fast.
![with-feature](/images/diagrams/brush-velocity-with-feature.webp)

**Implementation**: Simplified Dynamic Spacing Calculation - Removed the formula that scaled spacing up to 200%. Now, dynamic spacing is directly multiplied by `core->spacing`, ensuring a simpler and more predictable behavior. The minimum spacing is clamped to `EPSILON` to prevent it from becoming too small.

**Benefits**: The new approach provides cleaner, more predictable spacing behavior, adhering more closely to user-defined values without arbitrary limits.

</div>

---
