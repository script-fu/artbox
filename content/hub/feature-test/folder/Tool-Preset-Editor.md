# Objective

Enhance the Tool Preset Editor.

## Related Links

- Branches: [Artbox](https://gitlab.gnome.org/pixelmixer/artbox/-/tree/artbox?ref_type=heads)

## Design Revisions

| **Revision**               | **Current Design**                                           | **Issues**                                                                                             | **Changes**                                                                                               |
|----------------------------|--------------------------------------------------------------|--------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------|
| **1. Icon Picker Update**  | The icon picker is very small on a HDPI screen.             | Limited icon visibility, reducing ease of use and feature discovery.                                   | Added a new `icon_tool_preset` boolean property to adjust the picker size in the Tool Preset Editor, enlarging and centering the icon picker. |
| **2. Tool Preset Expander** | Tool Preset editor apply options are listed without context. | Lack of organization leads to a cluttered UI in the Tool Preset Editor and an oversized dock.          | Implemented an expandable frame grouping preset toggle options under "Preset Application Filter" for a cleaner, and minimum height, layout.                         |

## MR Description

This MR improves the tool preset editor's usability and enhances icon picker customization, focusing on visual improvements and configurable options for a more intuitive user experience.

### Changes

1. **Icon Picker Update**:
   - Added a new `icon_tool_preset` boolean property to conditionally adjust the picker size for the Tool Preset Editor.
   - The icon picker is placed in the center of the editor.

2. **Tool Preset Expander**:
   - Added a collapsible `Preset Application Filter` frame in the Tool Preset Editor to contain various preset options as checkboxes.
   - Used the GTK expander widget to create a compact interface that keeps options accessible while minimizing visual clutter.

### Benefit

- The enlarged icon picker and organized Tool Preset Editor improve visual feedback and provide a structured layout for managing complex tool configurations. The `Preset Application Filter` expander reduces interface clutter and reduces dock height, optimizing usability.
