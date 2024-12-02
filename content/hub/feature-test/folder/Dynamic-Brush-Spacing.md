---
type: docs
---

# Objective

Improve the quality of the brush spacing with respect to velocity.

## Design Revisions

| **Revision**  | **Current Design**  | **Issues**  | **Changes** |
|--------------------------------------------|---------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------|-----------------------------------------------------------|
| **1. Remove Spacing Limits**   | Spacing is set to 200% for fast | Spacing does not respect the Paint Tool slider settings | Spacing respects the slider values |

## Notes

This feature branch was a proposed solution to https://gitlab.gnome.org/GNOME/gimp/-/issues/1863

**Without Feature:** Top is a slow stroke, middle line fast, lower is slow to fast.
![without-feature](/images/diagrams/brush-velocity-without-feature.webp)

**With Feature:** Top is a slow stroke, middle line fast, lower is slow to fast.
![with-feature](/images/diagrams/brush-velocity-with-feature.webp)

### Changes

- **Simplified Dynamic Spacing Calculation**:
  - Removed the formula that scaled spacing up to 200%.
  - Now, dynamic spacing is directly multiplied by `core->spacing`, ensuring a simpler and more predictable behavior.
  - The minimum spacing is clamped to `EPSILON` to prevent it from becoming too small.

### **Benefits**

- The new approach provides cleaner, more predictable spacing behavior, adhering more closely to user-defined values without arbitrary limits.
