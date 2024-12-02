---
type: docs
---

# Objective

Make a beautiful brush stroke.

## Design Revisions

| **Revision**  | **Current Design**  | **Issues**  | **Changes** |
|--------------------------------------------|---------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------|-----------------------------------------------------------|
| **1. Apply a multiply to the dynamics output factor** | dynamic output is summed | Enforcing a fine start and end to the brush stroke, with multiple dynamic elements in play can be difficult or impossible to achieve.  | Paintbrush options to `Pressure Multiply` and `Fade Multiply` are available to be enabled. The pressure and fade dynamics can then be a defining factor on the overall character of the brush calligraphy. |

## Notes

**Feature:** The left side is with Pressure and Fade multiply enabled, right side is without
![feature](/images/diagrams/brush-dynamic-multiply-modes.webp)

### Changes

- **Pressure Dynamics**:
  - Added `options->brush_pressure_multiply` check.
  - If enabled and there are existing factors, the pressure is multiplied. Otherwise, it's added as usual.

- **Fade Dynamics**:
  - Added `options->fade_options->fade_multiply` check.
  - If enabled and there are existing factors, the fade is multiplied. Otherwise, it's added.

### **Benefits**

Allows users to multiply or add pressure and fade dynamics for more precise brush control.
