# Objective

Improve the usability of the Paintbrush GUI and create new stroke possibilities.

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
| **8. Jitter Slider** | New feature. | Jitter was under `Apply Jitter` down the options, using relative to brush size jittering | Added a 'Jitter' slider. |
| **9. Eraser Slider** | New feature. | Eraser size is same as brush size or unique to the eraser | Added an 'Eraser' slider to work with a custom plug-in that toggles to the eraser tool. The slider value is applied as a scale on the eraser brush size. This allows all the painting tool presets to have a specific sized eraser. Erase pencil lines with a big eraser, cut into brush strokes with a smaller eraser.|
| **10. Uniform Jitter** | New feature. | Jitter is has a natural bias towards the center point | Added an extra option in Additional Options called `Uniform Jitter`. When checked, the jitter is applied in a uniform manner |
| **11. Initial Angle** | New feature. | Needed to go from an initial angle to a directional angle over a fade in length | Added an extra options in Fade and Colour, one is a slider `Initial Angle` and the other is a checkbox `Fade Initial Angle`. A linear interpolation is done independently of the fade curve according to the fade length. |
| **12. Brush Angle Blend Factor** | New feature. | The final blend amount for the linear interpolation can be defined here | Added an extra options in Fade and Colour, a slider `Brush Angle Blend Factor`  |
| **13. Direction Stabilization** | New feature. | Delays the start of the stroke until we have some consistent stroke information to work with| Added an extra options in Fade and Colour, a slider `Direction Stabilization` the pixel distance from the click of the stroke starting to the paint being rendered. |
| **14. Relative Initial Angle** | New feature. | Use the initial angle as a relative offset to the direction angle.  | Added an extra options in Fade and Colour, `Use Relative Angle`. |
| **15. Random Angle** | A random angle always added to and angle | Needed a controllable random amount that could then be used to jitter clockwise and anticlockwise the current angle | The random curve graph for angles is used to intuitively control this. |

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

- **Jitter Slider**:
    - Added a 'Jitter' slider, it's an important feature for painting and feels great to have it as a slider.

- **Eraser Slider**:
    - Added an 'Eraser' slider to scale the eraser tool when it is toggled to using a custom Artbox plug-in. Now the painter can pair eraser sizes with tool sizes as part of a tool preset. Erase pencil lines with a big eraser, cut into brush strokes with a smaller eraser.
    Adjust the relationship as you work to shape the paint and erase the lines effectively, spend less time picking brush sizes.

- **Uniform Jitter**: 
  - Added an extra option in Additional Options called `Uniform Jitter`. When checked, any jitter is applied in a uniformly distributed way.

- **Reworked Angle Dynamics**:

Computes the final dymnamic brush angle for a paint operation, combining multiple input dynamics (pressure, velocity, direction, tilt, wheel, fade, and random jitter) according to the enabled options and user-defined curves.

Each enabled dynamic contributes an angle value in normalized [0,1) units, where 1.0 == 360°. These values are averaged to produce a base result.

If `Fade Initial Angle` is enabled, the result is smoothly blended from the initial brush angle to the computed dynamic angle over the stroke, using unit vector interpolation for shortest-path blending. The final blend amount can be defined with `Brush Angle Blend Factor`. Check `Use Relative Angle` to apply the initial angle as an offset relative to the active dynamic angle. To avoid an unstable start to the brush stroke, or to turn off the first click stamp, set `Direction Stabilization` to a value greater than 0.

Random angle jitter is applied last, as a small perturbation around the final angle. This is controlled by a user-editable curve in the GUI.

Usage notes:

- Enable or disable each dynamic (pressure, velocity, etc.) in the brush dynamics settings.

- Adjust the corresponding input curves to control how each input affects the angle.

- The "fade initial angle" option causes the stroke to start at the initial angle and transition to the dynamic angle as the stroke progresses.

- The random input curve should be centered around 0.5 for symmetric jitter.

- A straight line from 0.0 to 1.0 gives maximum jitter in both directions.

- A flat line at 0.5 gives no jitter.

- A line from 0.4 to 0.6 gives subtle jitter (±0.1 of the maximum).

### **Benefits**

This set of changes significantly improves the usability and efficiency of the Paintbrush GUI. By reducing visual clutter, hiding advanced options behind expanders, and simplifying the interface, users can now navigate the Paintbrush settings more easily while still accessing the features they need. The revised angle code and options open up a new range of stroke styles.