---
type: docs
url: "hub/feature-test/folder/Tool-Preset-Editor"
---

# Tool Preset Editor

Enhance the Tool Preset Editor.

## Design Revisions

{{< cards >}}
  {{< card link="#icon-picker-update" title="Icon Picker Update" subtitle="Enhanced icon picker size and visibility for HDPI screens." icon="view-grid" >}}
  {{< card link="#tool-preset-information-table" title="Tool Preset Information Table" subtitle="New information table displaying saved and active resource states." icon="table" >}}
  {{< card link="#resource-reloading-options" title="Resource Reloading Options" subtitle="Organized reloading options under collapsible frames." icon="refresh" >}}
  {{< card link="#linked-resource-saving-options" title="Linked Resource Saving Options" subtitle="New expandable frame for managing linked resource options." icon="save" >}}
  {{< card link="#linked-resource-save-as-feature" title="Linked Resource Save-As Feature" subtitle="Streamlined method for creating additional presets with named copies." icon="duplicate" >}}
{{< /cards >}}

---

<div class="feature-section" id="icon-picker-update">

## Icon Picker Update

**Current Design**: The icon picker is very small on HDPI screens.

**Issues**: Limited icon visibility reduces ease of use and impacts feature discoverability.

**Changes**: Added a new `icon_tool_preset` boolean property to adjust the icon picker size in the Tool Preset Editor. Enlarged and centered the icon picker for better visibility and usability.

</div>

---

<div class="feature-section" id="tool-preset-information-table">

## Tool Preset Information Table

**Current Design**: **New Feature**

**Issues**: Users lack insight into the saved and active states of resources linked to Tool Presets, hindering editing and creation workflows.

**Changes**: Implemented an information table that clearly displays the saved and active states of resources associated with Tool Presets.

</div>

---

<div class="feature-section" id="resource-reloading-options">

## Resource Reloading Options

**Current Design**: Tool Preset Editor options are listed without context.

**Issues**: Unorganized options create a cluttered interface and lead to an oversized dock, reducing efficiency.

**Changes**: Grouped related options under a collapsible "Resource Reloading" frame using an expandable widget. Added explanatory tooltips for clarity.

</div>

---

<div class="feature-section" id="linked-resource-saving-options">

## Linked Resource Saving Options

**Current Design**: **New Feature**

**Issues**: There are no options for managing linked resources when creating new Tool Presets.

**Changes**: Introduced an expandable "Linked Resource Saving" frame that provides toggleable options for managing linked resources. These options apply when saving Tool Presets or linked resources.

</div>

---

<div class="feature-section" id="linked-resource-save-as-feature">

## Linked Resource Save-As Feature

**Current Design**: **New Feature**

**Issues**: No streamlined method for creating additional presets with named copies of linked resources.

**Changes**: Added a "Save As" button and menu option to save linked resources with new names. Implemented a dialog that provides a guided workflow for naming and saving linked resources along with Tool Presets.

---

## Key Changes

- **Icon Picker Update**:
   - Added a new `icon_tool_preset` boolean property to dynamically adjust the icon picker's size in the Tool Preset Editor.
   - Enlarged and centered the icon picker for better usability on HDPI screens.

- **Tool Preset Information Table**:
   - Introduced an information table that displays both the saved and active states of resources linked to Tool Presets.
   - This provides users with clear insights into linked resource configurations, enhancing editing and creation workflows.

- **Resource Reloading Options**:
   - Consolidated the Tool Preset Editor's resource reloading options into a collapsible "Resource Reloading" frame using a GTK expander widget.
   - Added tooltips to clarify the purpose of each option, improving usability and reducing interface clutter.

- **Linked Resource Saving Options**:
   - Added a collapsible "Linked Resource Saving" frame for managing linked resource options when saving Tool Presets.
   - Ensures streamlined handling of linked resources for both new and existing presets.

- **Save-As Feature for Linked Resources**:
   - Introduced a "Save As" button and menu option for saving linked resources with new names.
   - Created an interactive dialog to guide users through naming linked resources and saving Tool Presets.


