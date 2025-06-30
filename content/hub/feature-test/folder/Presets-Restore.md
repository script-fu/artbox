---
type: docs
url: "hub/feature-test/folder/Presets-Restore"
---

# Presets Restore

Improve the usability of Tool Presets in Artbox.

## Design Revisions

{{< cards >}}
  {{< card link="#double-click-active-preset-to-restore" title="Double Click Active Preset to Restore" subtitle="Quick restoration of active preset settings with double-click." icon="refresh" >}}
{{< /cards >}}

---

<div class="feature-section" id="double-click-active-preset-to-restore">

## Double Click Active Preset to Restore

**Current Design**: Clicking an active preset has no affect

**Issues**: User has to select another preset then reselect to restore options to the save preset

**Current Design**: Clicking on an already active preset has no effect.

**Issues**: Users must select a different preset before reselecting the desired one to restore its settings, creating unnecessary steps.

**Changes**: Double clicking restores the preset immediately.

**Implementation**: The `gimp_container_icon_view_item_activated` function was updated to call `gimp_context_tool_preset_changed` when a preset is double-clicked, restoring the preset's tool options instantly and eliminating the need for multi-step workflows.

**Benefits**: Simplifies the process of restoring Tool Preset options, providing a more efficient workflow and improved user experience through direct preset restoration.

</div>

---
