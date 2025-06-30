---
type: docs
url: "hub/feature-test/folder/Selection-Display"
---

# Objective

Improve the quality of the painting experience in Artbox by enhancing the active selection behavior.

## Design Revisions

{{< cards >}}
  {{< card link="#selection-mask-highlighting" title="Selection Mask Highlighting" subtitle="Shaded overlay for unselected areas" icon="eye" >}}
  {{< card link="#select-all-highlighting" title="Select All Highlighting" subtitle="Visual indication of Select All state" icon="selector" >}}
  {{< card link="#selection-borders" title="Selection Borders" subtitle="Adjustable border thickness and style" icon="adjustments" >}}
  {{< card link="#selection-status" title="Selection Status" subtitle="Status bar indication for invisible selections" icon="information-circle" >}}
{{< /cards >}}

---

<div class="feature-section" id="selection-mask-highlighting">

## Selection Mask Highlighting

**Current State**: Rectangle selection highlighting is on a few tools, and is not global.

**Issue**: Knowing if there is an active selection can be an issue. Working without selection borders becomes difficult. Changing tools loses the selection highlighting.

**Solution**: Draw a shaded overlay that masks out unselected areas. Additional preference options for the shade alpha and colour. Additional View option 'Show Selection Highlight' to toggle with a shortcut to quickly turn off and on.

**Implementation**: Implemented a global shaded overlay system that masks unselected areas with customizable transparency and color. Added preference controls for shade alpha and color customization, plus a View menu option 'Show Selection Highlight' with keyboard shortcut support for quick toggling.

**Benefits**: Allows users to work without selection borders while maintaining clear visual indication of selected areas. The accurate selection area shading makes it intuitive to understand what content is editable, improving the painting experience across all tools.

</div>

<div class="feature-section" id="select-all-highlighting">

## Select All Highlighting

**Current State**: No clear indication of a `Select All` state.

**Issue**: Knowing if there is an active select all can be an issue.

**Solution**: Draw a shaded frame on the canvas padding that indicates select all.

**Implementation**: Implemented a visual frame system that draws a shaded border around the canvas padding area when Select All is active, providing clear visual feedback for this common selection state.

**Benefits**: Provides immediate visual confirmation when Select All is active, eliminating uncertainty about the current selection state and improving workflow clarity.

</div>

<div class="feature-section" id="selection-borders">

## Selection Borders

**Current State**: New Feature.

**Issue**: No way to adjust the thickness or harshness of selection borders.

**Solution**: Added preferences to adjust the selection border.

**Implementation**: Added comprehensive preference controls for selection border customization, allowing users to adjust both thickness and visual intensity of selection borders to match their workflow preferences.

**Benefits**: Enables personalized selection border appearance, allowing users to work with softer or more prominent borders based on their visual preferences and workflow requirements.

</div>

<div class="feature-section" id="selection-status">

## Selection Status

**Current State**: New Feature.

**Issue**: When 'Show Selection', and in Artbox 'Show Selection Highlight' are off, no indication of an active selection is given.

**Solution**: Added a Status Bar label that indicates when there is an 'invisible' selection.

**Implementation**: Implemented a status bar indicator that displays when an active selection exists but is not visually represented due to disabled selection visibility options.

**Benefits**: Enables users to paint selection areas without any obscuring visual indicators on the image while still receiving confirmation of active selections through the status bar. This is particularly useful when working with precise selections that require unobstructed canvas view.

**Settings**:
- Edit > Preferences > Image Windows > Selection Highlighting
- View > Show Selection Highlight

**Demo**: Video on [YouTube](https://youtu.be/RG3rOhjXXW0)

</div>


