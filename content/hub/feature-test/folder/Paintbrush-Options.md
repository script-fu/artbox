# Objective

Improve the usability of the Paintbrush GUI.

## Design Revisions

| **Revision** | **Current Design** | **Issues** | **Changes** |
|--------------|---------------------|------------|-------------|
| **1. Adapt Reset Brush Button** | Option sliders have a reset button to default brush values. | Rarely used in some workflows; adds complexity to the GUI. | Make it optional via a Tool Options -> Paintbrush preference. Also, <kbd>Ctrl + Click</kbd> on the slider to reset it to the brush default. |
| **2. Adapt Brush Link Button** | Brush link button allows linking to brush editor options and brush changes. | Difficult to explain and used in some workflows, not all; causes confusion. | Rename the button to Brush Update Button. Make it optional via a Tool Options -> Paintbrush preference. Add more clarity and information to the tooltip. |
| **3. Add Expander for Additional Options** | Options are added to the end of Paintbrush settings; more options will be added in the future. | Lesser-used options clutter the interface and reduce dock space efficiency. | Add an "Additional Options" expander for lesser-used items. |
| **4. Separate Dynamics** | 'Enable Dynamics' contains the 'Fade and Colour' options. | The 'Fade and Colour' options take up a lot of space and do not need to be visible all the time. | Add a "Dynamic Fade and Colour" expander, visible only when Enable Dynamics is checked. |
| **5. Compact Resource Chooser** | Picking a resource such as a brush or a dynamic is done via a chooser in the Paintbrush GUI. | The chooser takes up two rows of the dockable panel due to a label above the combo box. The icons on either side are distorted to fill the gap, which looks poor. GUI space is wasted. | Remove the label to make the chooser more compact. The purpose of the chooser is self-evident and does not need a label. |
| **6. Smooth Stroke Position** | 'Smooth Stroke' is located lower down in the dock. | It’s a frequently used option for painting. | Move it higher up in the dock within 'Stroke Effects'. |
| **7. Stroke Effects Expander** | New feature. | Options clutter the Paintbrush GUI, or don't flow visually. | Create a 'Stroke Effects' expander to organize these related options. The state of the expander is saved and restored. |
| **8. Pick Layer** | New feature. | It's difficult to find layers in complex layer stacks | Added an option in `Additional Options` to `Pick Layer`. The layer under the brush is selected when Alt is pressed.  |

### Changes

- **Remove Reset Brush Button**:
    - Made the `Reset to brush default` buttons optional. Added a new feature to <kbd>Ctrl + Right Click</kbd> to also reset the Tool Option to the brush defined setting.

- **Remove Brush Link Button**:
    - Made the 'Link to Brush Editor' button optional, which previously allowed linking the Paintbrush options to the Brush Editor options. This simplifies the GUI for those that do not use this feature. 
- **Add Expander for Additional Options**:
    - Introduced a new "Additional Options" expander in the Paintbrush options panel. This organizes less frequently used options (such as 'Lock Brush to View' and 'Simple Brush Boundary' toggles) into a collapsible section, saving space and reducing clutter in the GUI.

- **Separate Dynamics (Fade and Colour)**:
    - Moved the 'Fade and Colour' options (related to brush dynamics) into a separate expander that appears only when 'Enable Dynamics' is checked. This keeps the interface cleaner by hiding these advanced options when dynamics are not in use.
    - Added `fade-multiply` and `brush-pressure-multiply` toggles to enable pressure and fade dynamics, providing more fine-tuned control.

- **Compact Resource Chooser**:
    - Removed the label from the resource chooser (used for selecting brushes, dynamics, etc.), making the chooser more compact and saving space in the dockable panel. The chooser’s function is self-explanatory, so the label was deemed unnecessary.

- **Smooth Stroke Position**:
    - Moved the 'Smooth Stroke' options higher up in the Paintbrush options panel, reflecting its frequent use. This improves accessibility and better aligns with user expectations.

- **Stroke Effects Expander**:
    - Added a new "Stroke Effects" expander to group related stroke options into one collapsible section. The state of the expander is saved and restored across sessions, preserving the user's preference for a consistent experience.

- **Pick Layer**:
    - Added a new "Pick Layer" option in the **Additional Options** expander. This feature allows users to hold the <kbd>Alt</kbd> key to automatically select the layer under the brush cursor. This option simplifies workflows with complex layer stacks by enabling quick access to the correct layer without manually searching through the layers panel.

### **Benefits**

This set of changes significantly improves the usability and efficiency of the Paintbrush GUI. By reducing visual clutter, hiding advanced options behind expanders, and simplifying the interface, users can now navigate the Paintbrush settings more easily while still accessing the features they need.

`Pick Layer` reduces layer stack searching and will be improved to handle multiple layers under the cursor in the future.
