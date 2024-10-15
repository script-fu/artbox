---
type: docs
---

# Objective

Make sense of the mapping graphs for dynamic features by removing the velocity inversion.

## Related Links

- Branches: Artbox and [feature-remove-inverted-dynamic-velocity](https://gitlab.gnome.org/pixelmixer/artbox/-/tree/feature-remove-inverted-dynamic-velocity?ref_type=heads)

## Design Revisions

| **Revision**  | **Current Design**  | **Issues**  | **Changes** |
|--------------------------------------------|---------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------|-----------------------------------------------------------|
| **1. Remove Velocity Inversion** | Velocity is math inverted | The max and min values are inverted in the spacing curve graph  | The velocity math is not inverted and the graph for velocity mapping is accurate |

## MR Description

This MR removes the velocity inversion in the dynamic features, ensuring the velocity mapping is more intuitive and accurate.

### Changes

- **Remove Velocity Inversion**:
  - The velocity is no longer inverted (`1.0 - coords->velocity` removed).
  - Now, `coords->velocity` is mapped directly, making the graph for velocity mapping more accurate.

### Benefit

- This change ensures that the velocity mapping in the dynamic features behaves correctly, making it easier for users to understand and control their brush settings without inverted values.
