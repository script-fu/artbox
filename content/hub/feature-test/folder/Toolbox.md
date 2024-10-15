---
type: docs
---

# Objective

Improve the usability of the Toolbox.

## Key Concepts and Definitions

- **Flowbox**: A flexible container that one to three widgets are arranged in. The FG/BG colour area, the active resources and active image.
- **Tool Palette**: The grid of tool buttons, Move Tool, Paintbrush Tool ect.
- **FG/BG**: The active foreground & background colour widget.

## Related Links

- Branches: Artbox and [feature-toolbox](https://gitlab.gnome.org/pixelmixer/artbox/-/tree/feature-toolbox?ref_type=heads)

## Revised Preferences

- Preferences -> Toolbox -> Appearance
  - Show colour, active resources and active image
  - Show only colour, set preferred position and scale.
    - Toolbox placement relative to the tool buttons
      - Top
      - Bottom
      - Left
      - Right
  - Scale the colour widget

## Design Revisions

| **Revision**  | **Current Design**  | **Issues**  | **Changes** |
|--------------------------------------------|---------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------|-----------------------------------------------------------|
| **1. Remove Flowbox** | The Flowbox is positioned beneath the Tool Palette | The Flowbox takes up a large amount of GUI space. If only one or two elements are preferred, the GUI space is empty. The size of the FG/BG is restricted by the arrangement.| Allow the user to create a simpler toolbox with no wasted space by removing the Flowbox and keeping the FG/BG widget |
| **2. Position and scale the FG/BG widget.**   |  New Feature | The FG/BG widget may be poorly positioned taking up GUI space. It may be too small on HDPI displays | Allow the user to position and scale the FG/BG widget relative to the Tool Palette |

## MR Description

This MR enhances the usability of the Toolbox in Artbox by introducing options for greater customization of the UI, specifically around the Flowbox and FG/BG widget.

### Changes

1. **Optional Removal of Flowbox**:
   - The Flowbox, which arranges active resources, FG/BG color widget, and active image beneath the Tool Palette, is now optional. Users can choose to keep or remove the Flowbox based on their preferences.
   - Removing the Flowbox allows for a more compact and efficient Toolbox layout by eliminating empty space when fewer elements are displayed.

2. **Position and Scale FG/BG Widget**:
   - The FG/BG color widget can now be positioned (Top, Bottom, Left, or Right) relative to the Tool Palette. This improves layout flexibility and user customization.
   - The FG/BG widget can also be scaled, providing better usability for HDPI displays or different screen configurations.

3. **Revised Toolbox Preferences**:
   - Added preferences in the Toolbox Appearance settings:
     - Control over showing the Flowbox with color, active resources, and active image.
     - Set the preferred position of the FG/BG widget relative to the Tool Palette.
     - Option to scale the FG/BG widget to fit different display settings.

### Technical Details

- **toolbox_create_flexible_fg_bg**: 
  - A new function introduced to allow the FG/BG widget to be positioned and scaled outside of the Flowbox, if the user opts to remove the Flowbox.

- **toolbox_create_flowbox**:
  - This function retains the default layout, including the Flowbox, if the user chooses to keep it.

- **gimp_tool_palette_style_updated**:
  - Adjustments made to handle scaling and positioning logic of the FG/BG widget based on user preferences, ensuring consistency across various layouts.

### Benefit

- These updates provide users with a choice between a simplified, compact Toolbox or the existing flexible layout, offering better control over the user interface. Scaling and positioning options make the Toolbox adaptable to different display sizes and user preferences, leading to a more efficient workflow.
