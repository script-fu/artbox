---
type: docs
url: "hub/feature-test/folder/Dynamic-Multiply-Modes"
---

# Objective

Make a beautiful brush stroke.

## Design Revisions

{{< cards >}}
  {{< card link="#pressure-fade-multiply" title="Dynamic Multiply Modes" subtitle="Enhanced brush stroke control" icon="beaker" >}}
{{< /cards >}}

---

<div class="feature-section" id="pressure-fade-multiply">

## Dynamic Multiply Modes

**Current State**: Dynamic output is summed.

**Issue**: Enforcing a fine start and end to the brush stroke, with multiple dynamic elements in play can be difficult or impossible to achieve.

**Solution**: Paintbrush options to `Pressure Multiply` and `Fade Multiply` `Fade Multiply Angular` `Fade Multiply Ratio` are available to be enabled. The pressure and fade dynamics can then be a defining factor on the overall character of the brush calligraphy.

**Feature Demonstration**: The left side is with Pressure and Fade multiply enabled, right side is without
![feature](/images/diagrams/brush-dynamic-multiply-modes.webp)

**Implementation Changes**:

- **Pressure Dynamics**: Added `options->brush_pressure_multiply` - If enabled and there are existing factors, other factors are multiplied by the pressure. Otherwise, it's added as usual.

- **Fade Dynamics**: Added `options->fade_options->fade_multiply`, `options->fade_options->fade_multiply_angular`, and `options->fade_options->fade_multiply_ratio`

</div>

---

### **Benefits**

Allows users to multiply or add pressure and fade dynamics for more precise brush control.
