---
type: docs
---

# Objective

Improve the quality of the painting experience in Artbox

## Design Revisions

| **Revision**  | **Current Design**  | **Issues**  | **Changes** |
|--------------------------------------------|---------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------|-----------------------------------------------------------|
| **1. Easy Cursor Location** | The Tool Cursor can be turned off in Preferences, and the pointer, leaving the only the brush outline. This is good, but causes issues. | A small and minimal cursor can be hard to locate | There is a minimum screen size for the cursor, and a small 'filled' 'contact' circle is always drawn |
| **2. Indicate Erase Mode**   | New Feature | It's not possible to tell if the paintbrush is about to erase whilst looking at the cursor | Detect the 'Eraser Tool' and 'Erase Paint' mode, change the cursor to a dashed circle |
| **3. Simple Brush Boundary**   | Image brushes are drawn as complex outlines based on the image | They can make a distracting paintbrush when the image is large and noisy  | Draw a simple circular boundary if the 'Simple Brush Boundary' option is checked in the Paintbrush Options |

### Changes

- **Easy Cursor Location**:
     - Introduced a new function `gimp_draw_brush_cursor` that ensures a minimum cursor size, even when the brush is very small or not visible (e.g., zero-pressure).
     - Defined constants `FINDER_SIZE` and `CORE_SIZE` to ensure a small 'filled' contact circle is always drawn, making the cursor easier to locate.
     - If the brush outline is too small, `should_locate` triggers a fallback locator circle.

- **Indicate Erase Mode**:
     - The new `gimp_is_erasing_paint` function detects when the user is in 'Eraser Tool' mode or the 'Erase Paint' blending mode.
     - When erasing is active, the cursor switches to a dashed circle by invoking `gimp_draw_arc_circle`, providing clear visual feedback.
     - A small filled circle is also drawn at the center to help users identify the brush's contact point.

- **Simple Brush Boundary**:
     - Added a new boolean option `brush_simple_boundary` in the Paintbrush Options GUI.
     - In the `gimp_paint_tool_draw` function, the standard complex outline of the brush (derived from the image brush mask) is bypassed when this option is enabled.
     - Instead, a simple circular boundary is drawn by the `draw_brush_circle` function, providing a cleaner, less noisy visual representation for large or complex brushes.

### **Benefits**

- These updates improve the visual clarity and feedback of the brush cursor during painting. The small contact circle ensures the cursor is always visible, the dashed circle gives clear feedback in erase mode, and the simple brush boundary reduces distractions from complex brush shapes.
