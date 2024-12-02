---
type: docs
---

# Objective

Improve the usability of Tool Presets in Artbox.

## Design Revisions

| **Revision**  | **Current Design**  | **Issues**  | **Changes** |
|--------------------------------------------|---------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------|-----------------------------------------------------------|
| **1. Double click active preset to restore** | Clicking an active preset has no affect | User has to select another preset then reselect to restore options to the save preset | Double clicking restores the preset. |

### Changes

1. **Double-Click to Restore Active Preset**:
     - Previously, clicking on an already active preset had no effect, requiring the user to select a different preset before selecting the desired one to restore its settings.
     - The `gimp_container_icon_view_item_activated` function was updated to call `gimp_context_tool_preset_changed` when a preset is double-clicked, restoring the preset's tool options immediately.

### **Benefits**

- This change simplifies the process of restoring Tool Preset options, providing a more efficient workflow by eliminating unnecessary clicks. Now, double-clicking an active preset will quickly restore its saved settings, improving the overall user experience.
