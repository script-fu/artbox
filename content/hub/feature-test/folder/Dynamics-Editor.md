---
type: docs
url: "hub/feature-test/folder/Dynamics-Editor"
---

# Dynamics Editor

Enhance the Dynamics Editor.

{{< cards >}}
  {{< card link="#mapping-matrix" title="Mapping Matrix" subtitle="Improved layout and scrollability" icon="view-grid" >}}
  {{< card link="#reset-confirmation" title="Reset Confirmation" subtitle="Protect against accidental data loss" icon="exclamation-circle" >}}
  {{< card link="#copy-paste-curves" title="Copy and Paste Curves" subtitle="Reuse and share curve data" icon="duplicate" >}}
  {{< card link="#dynamic-attributes" title="Dynamic Attributes" subtitle="Scrollable treeview interface" icon="collection" >}}
{{< /cards >}}

---

<div class="feature-section" id="mapping-matrix" tabindex="-1">

## Mapping Matrix

**Current Design**: See GIMP Dynamics Editor

**Issues**: Awkward labels like `Aspect Ratio` and `Rotation/Wheel` detract from the interface. Checkboxes lack margins, causing labels to overlap. The Mapping Matrix is not scrollable, making the Dynamics Editor dock excessively large and difficult to reduce in size. The large array of checkboxes complicates identification of their function.

**Changes**: Renamed awkward labels, added margins around checkboxes, added tooltips for each checkbox, and enclosed the Mapping Matrix in a scrollable window.

**Benefits**: 
- Renamed awkward labels like `Aspect Ratio` and `Rotation/Wheel` for clarity
- Added margins to checkboxes to prevent label overlap and improve layout consistency
- Included tooltips for each checkbox to explain its function
- Enclosed the Mapping Matrix in a scrollable window, reducing the minimum size of the Dynamics Editor dock and enhancing interface flexibility

</div>

<div class="feature-section" id="reset-confirmation" tabindex="-1">

## Reset Confirmation

**Current Design**: See GIMP Dynamics Editor

**Issues**: Reset Curve removes user data without warning, leading to potential accidental loss of work.

**Changes**: Added a confirmation dialog that prompts users before resetting curves, reducing the risk of unintended data loss.

**Benefits**: Implemented a confirmation dialog that warns users before resetting curves. This ensures that user data is not lost unintentionally, improving overall reliability.

</div>

<div class="feature-section" id="copy-paste-curves" tabindex="-1">

## Copy and Paste Curves

**Current Design**: There is no way to copy a curve.

**Issues**: Lack of copy functionality makes it difficult to reuse or transfer curve data, reducing workflow efficiency.

**Changes**: Added `Copy Curve` and `Paste Curve` buttons. Curves are saved as text files, enabling persistence between sessions and easy sharing.

**Benefits**: 
- Introduced `Copy Curve` and `Paste Curve` buttons for reusing and sharing curve data
- Enabled saving curve points to text files, allowing persistence between sessions and simplifying data management

</div>

<div class="feature-section" id="dynamic-attributes" tabindex="-1">

## Dynamic Attributes

**Current Design**: See GIMP Dynamics Editor

**Issues**: The Dynamic Attributes treeview is not in a scrollable window, making the Dynamics Editor dock excessively large and inflexible.

**Changes**: Enclosed the Dynamic Attributes treeview in a scrollable window to improve layout flexibility and reduce dock size.

**Implementation**: Implemented scrollable window containers for the Dynamic Attributes treeview, enabling compact dock sizing while maintaining full functionality access.

**Benefits**: Provides a more flexible interface layout that reduces dock size constraints, allowing users to customize their workspace more effectively while maintaining easy access to all dynamic attributes.

</div>



