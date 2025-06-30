---
type: docs
url: "hub/feature-test/folder/Color-Picker-Tool"
---

# Color Picker Tool

Improve the Color Picker Tool

{{< cards >}}
  {{< card link="#alt-key-toggles-sample-merged" title="Alt Key Toggles Sample Merged" subtitle="Temporary toggle for sample mode" icon="color-swatch" >}}
{{< /cards >}}

---

<div class="feature-section" id="alt-key-toggles-sample-merged" tabindex="-1">

## Alt Key Toggles Sample Merged

**Current Design**: New Feature

**Issues**: Never know what state the sample option was left in

**Changes**: Whilst `Alt` is pressed toggle the Sample Merged state

**Benefits**: The user can set the default state for the Sample Merged option in the Color Picker Tool as needed, and it will stay in that state. For example, when using `Ctrl` to pick while painting (which follows the current state of the Color Picker Tool), Sample Merged is turned off by default. If you want to sample merged, select the Color Picker Tool and hold Alt while picking. This method removes the unpredictable changes in the sampling method of the picker tool.

</div>
