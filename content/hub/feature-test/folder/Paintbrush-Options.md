---
type: docs
---

# Objective

Improve the usability of the Paintbrush GUI.

## Key Concepts and Definitions

- **Reset Brush Option**: Resets the slider to a default value.
- **Brush Link Button**: Links the paintbrush options to the brush editor options.
- **Expander**: A collapsible GUI section for organizing lesser-used options.

## Related Links

- Branches: Artbox and [feature-paintbrush-options](https://gitlab.gnome.org/pixelmixer/artbox/-/tree/feature-paintbrush-options?ref_type=heads)

## Design Revisions

| **Revision**  | **Current Design**  | **Issues**  | **Changes** |
|--------------------------------------------|---------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------|-----------------------------------------------------------|
| **1. Remove Reset Brush Button** | Option sliders have a reset button to default values. | Rarely used; adds complexity to the GUI. | Remove the reset to default button. |
| **2. Remove Brush Link Button**   | Brush link button allows linking to brush editor options. | Difficult to explain and justify; causes confusion | Remove the link button. |
| **3. Add Expander for Additional Options** | Options added to the end of paintbrush settings; more options will be added in the future   | Lesser-used options clutter the interface and reduce dock space efficiency | Add an "Additional Options" expander for lesser-used items |
| **4. Separate Dynamics** | 'Enable Dynamics' contains the 'Fade and Colour' options| The 'Fade and Colour' options take up a lot of space, and do not need to be visible all the time.| Add a "Dynamic Fade and Colour" expander, visible when Enable Dynamics is checked |
| **5. Compact Resource Chooser** | Picking a resource such as a brush or a dynamic is done via a chooser, see the Paintbrush GUI | The chooser is takes up two rows of the dockable due to a label above the combo box. The icons on either side are distorted to fill the gap, which looks bad. GUI space is wasted | Remove the label and the chooser becomes compact. The purpose of the chooser is self evident and does not need a label|
| **6.Smooth Stroke Position** | 'Smooth Stroke' is in low down in the dock | It's a frequently used option for painting | Move higher up the dock |

## MR Description

This MR enhances the Paintbrush GUI in several ways, making it more intuitive and streamlined by removing unnecessary elements and organizing options more efficiently.

### Changes

1. **Remove Reset Brush Button**:
     - Removed the reset buttons for brush size, aspect ratio, angle, spacing, and hardness from the Paintbrush options. The code for resetting these properties, along with the corresponding signals, was removed to simplify the interface.

2. **Remove Brush Link Button**:
     - Removed the 'Link to Brush Editor' button, which previously allowed linking the paintbrush options to the brush editor options. This simplifies the GUI by removing a confusing feature that was rarely used.

3. **Add Expander for Additional Options**:
     - Introduced a new "Additional Options" expander in the Paintbrush options panel. This organizes less frequently used options (such as the 'Lock Brush to View' and 'Simple Brush Boundary' toggles) into a collapsible section, saving space and removing clutter from the GUI.

4. **Separate Dynamics (Fade and Colour)**:
     - Moved the 'Fade and Colour' options (related to brush dynamics) into a separate expander that appears only when 'Enable Dynamics' is checked. This keeps the interface cleaner by hiding these advanced options when dynamics are not in use.
     - Added `fade-multiply` and `brush-pressure-multiply` toggles to enable pressure and fade dynamics, providing more fine-tuned control.

5. **Compact Resource Chooser**:
     - Removed the label from the resource chooser (used for selecting brushes, dynamics, etc.), making the chooser more compact and saving space in the dockable panel. The chooser’s function is self-explanatory, so the label was deemed unnecessary.

6. **Smooth Stroke Position**:
     - Moved the 'Smooth Stroke' options higher up in the Paintbrush options panel, reflecting its frequent use. This improves accessibility and better aligns with user expectations.

### Benefit

- This set of changes significantly improves the usability and efficiency of the Paintbrush GUI. By reducing visual clutter, hiding advanced options behind expanders, and simplifying the interface, users can now navigate the Paintbrush settings more easily while still accessing the features they need.
