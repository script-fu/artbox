---
type: docs
url: "hub/feature-test/folder/Dynamic-Multiply-Modes"
---

# Objective

Make a beautiful brush stroke.

## Design Revisions

| **Revision**  | **Current Design**  | **Issues**  | **Changes** |
|--------------------------------------------|---------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------|-----------------------------------------------------------|
| **1. Apply a multiply to the dynamics output factor** | dynamic output is summed | Enforcing a fine start and end to the brush stroke, with multiple dynamic elements in play can be difficult or impossible to achieve.  | Paintbrush options to `Pressure Multiply` and `Fade Multiply` `Fade Multiply Angular` `Fade Multiply Ratio` are available to be enabled. The pressure and fade dynamics can then be a defining factor on the overall character of the brush calligraphy. |

## Notes

**Feature:** The left side is with Pressure and Fade multiply enabled, right side is without
![feature](/images/diagrams/brush-dynamic-multiply-modes.webp)

### Changes

- **Pressure Dynamics**:
  - Added `options->brush_pressure_multiply`
If enabled and there are existing factors, other factors are multiplied by the pressure. Otherwise, it's added as usual.

- **Fade Dynamics**:
  - Added `options->fade_options->fade_multiply`
  - Added `options->fade_options->fade_multiply_angular`
  - Added `options->fade_options->fade_multiply_ratio`


### **Benefits**

Allows users to multiply or add pressure and fade dynamics for more precise brush control.
