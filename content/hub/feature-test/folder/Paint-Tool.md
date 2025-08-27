---
type: docs
url: "hub/feature-test/folder/Paint-Tool"
---

# Paint Tool

Improve the quality of the painting experience in Artbox

## Design Revisions

{{< cards >}}
  {{< card link="#easy-cursor-location" title="Easy Cursor Location" subtitle="Minimum cursor size and visibility improvements" icon="cursor-click" >}}
  {{< card link="#indicate-erase-mode" title="Indicate Erase Mode" subtitle="Visual feedback for erase operations" icon="trash" >}}
  {{< card link="#simple-brush-boundary" title="Simple Brush Boundary" subtitle="Clean circular boundaries for complex brushes" icon="pencil" >}}
  {{< card link="#eraser-tool-erases-on-mask" title="Eraser Tool on Mask" subtitle="Proper erasing behavior on layer masks" icon="eye-off" >}}
{{< /cards >}}

### Detailed Changes

<div class="feature-section" id="easy-cursor-location">

#### 1. Easy Cursor Location

- **Current Design**: The Tool Cursor can be turned off in Preferences, and the pointer, leaving the only the brush outline. This is good, but causes issues.
- **Issues**: A small and minimal cursor can be hard to locate.
- **Changes**: There is a minimum screen size for the cursor, and a small 'filled' 'contact' circle is always drawn.
- **How to Use**: 
  - Introduced a new function `gimp_draw_brush_cursor` that ensures a minimum cursor size
  - Defined constants `FINDER_SIZE` and `CORE_SIZE` to ensure a small 'filled' contact circle is always drawn
  - If the brush outline is too small, `should_locate` triggers a fallback locator circle
- **Benefits**: Makes the cursor easier to locate, even when the brush is very small or not visible.

</div>

<div class="feature-section" id="indicate-erase-mode">

#### 2. Indicate Erase Mode

- **Current Design**: New Feature
- **Issues**: It's not possible to tell if the paintbrush is about to erase whilst looking at the cursor.
- **Changes**: Detect the 'Eraser Tool' and 'Erase Paint' mode, change the cursor to a dashed circle.
- **How to Use**: 
  - The new `gimp_is_erasing_paint` function detects when the user is in 'Eraser Tool' mode or the 'Erase Paint' blending mode
  - When erasing is active, the cursor switches to a dashed circle by invoking `gimp_draw_arc_circle`
  - A small filled circle is also drawn at the center to help users identify the brush's contact point
- **Benefits**: Provides clear visual feedback about erase mode, preventing accidental erasure.

</div>

<div class="feature-section" id="simple-brush-boundary">

#### 3. Simple Brush Boundary

- **Current Design**: Image brushes are drawn as complex outlines based on the image.
- **Issues**: They can make a distracting paintbrush when the image is large and noisy.
- **Changes**: Draw a simple circular boundary if the 'Simple Brush Boundary' option is checked in the Paintbrush Options.
- **How to Use**: Enable 'Simple Brush Boundary' option in the Paintbrush Options for cleaner cursor display.
- **Benefits**: Reduces visual distraction from complex brush outlines, providing a cleaner painting experience.

</div>

<div class="feature-section" id="eraser-tool-erases-on-mask">

#### 4. Eraser Tool Erases on a Mask

- **Current Design**: Eraser uses the background colour, usually white on a mask.
- **Issues**: This is the opposite of erasing on a mask.
- **Changes**: The Eraser uses black on a mask.
- **How to Use**: Eraser tool automatically uses appropriate color when working on layer masks.
- **Benefits**: Proper erasing behavior on layer masks, making mask editing more intuitive.

</div>
