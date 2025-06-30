---
type: docs
url: "hub/feature-test/folder/Toolbox"
---

# Toolbox

Improve the usability of the Toolbox.

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

{{< cards >}}
  {{< card link="#remove-flowbox" title="Remove Flowbox" subtitle="Optional removal of Flowbox for more compact toolbox layout." icon="view-list" >}}
  {{< card link="#position-and-scale-fg-bg-widget" title="Position and Scale FG/BG Widget" subtitle="Flexible positioning and scaling for better display adaptation." icon="color-swatch" >}}
{{< /cards >}}

---

<div class="feature-section" id="remove-flowbox">

## Remove Flowbox

**Current Design**: The Flowbox is positioned beneath the Tool Palette

**Issues**: The Flowbox takes up a large amount of GUI space. If only one or two elements are preferred, the GUI space is empty. The size of the FG/BG is restricted by the arrangement.

**Changes**: Allow the user to create a simpler toolbox with no wasted space by removing the Flowbox and keeping the FG/BG widget

**Implementation**: The Flowbox, which arranges active resources, FG/BG color widget, and active image beneath the Tool Palette, is now optional. Users can choose to keep or remove the Flowbox based on their preferences, allowing for a more compact and efficient Toolbox layout when fewer elements are displayed.

**Benefits**: Provides users with a choice between a simplified, compact Toolbox or the existing flexible layout, offering better control over the user interface and eliminating wasted space.

---

<div class="feature-section" id="position-and-scale-fg-bg-widget">

## Position and Scale FG/BG Widget

**Current Design**: New Feature

**Issues**: The FG/BG widget may be poorly positioned taking up GUI space. It may be too small on HDPI displays

**Changes**: Allow the user to position and scale the FG/BG widget relative to the Tool Palette

**Implementation**: The FG/BG color widget can now be positioned (Top, Bottom, Left, or Right) relative to the Tool Palette and scaled for different display configurations. Added preferences in the Toolbox Appearance settings for complete customization control.

**Benefits**: Scaling and positioning options make the Toolbox adaptable to different display sizes and user preferences, leading to a more efficient workflow and better usability for HDPI displays.

</div>

---
