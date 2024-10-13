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
