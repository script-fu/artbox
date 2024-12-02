---
type: docs
---

# Objective

Remove the velocity inversion, so that the dynamic mapping graphs representation is accurate.

## Design Revisions

| **Revision**  | **Current Design**  | **Issues**  | **Changes** |
|--------------------------------------------|---------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------|-----------------------------------------------------------|
| **1. Remove Velocity Inversion** | The velocity calculations are inverted | The maximum and minimum values are inverted in the spacing curve graph  | The velocity calculations are no longer inverted, and the velocity mapping graph is accurate |

### Changes

- **Remove Velocity Inversion**:
  - The velocity is no longer inverted (`1.0 - coords->velocity` removed).
  - `coords->velocity` is mapped directly, making the graph for velocity mapping more accurate.

### **Benefits**

- This change corrects the velocity mapping in dynamic features, helping users understand and control brush settings without dealing with inverted values.
