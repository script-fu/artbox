# Objective

Enhance the Tool Preset Editor.

### **Design Revisions**

| **Revision**               | **Current Design**                                           | **Issues**                                                                                             | **Changes**                                                                                               |
|----------------------------|--------------------------------------------------------------|--------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------|
| **1. Icon Picker Update**  | The icon picker is very small on HDPI screens.              | Limited icon visibility reduces ease of use and impacts feature discoverability.                        | Added a new `icon_tool_preset` boolean property to adjust the icon picker size in the Tool Preset Editor. Enlarged and centered the icon picker for better visibility and usability. |
| **2. Tool Preset Information Table** | **New Feature** | Users lack insight into the saved and active states of resources linked to Tool Presets, hindering editing and creation workflows. | Implemented an information table that clearly displays the saved and active states of resources associated with Tool Presets. |
| **3. Resource Reloading Options** | Tool Preset Editor options are listed without context. | Unorganized options create a cluttered interface and lead to an oversized dock, reducing efficiency.   | Grouped related options under a collapsible "Resource Reloading" frame using an expandable widget. Added explanatory tooltips for clarity. |
| **4. Linked Resource Saving Options** | **New Feature** | There are no options for managing linked resources when creating new Tool Presets.                     | Introduced an expandable "Linked Resource Saving" frame that provides toggleable options for managing linked resources. These options apply when saving Tool Presets or linked resources. |
| **5. Linked Resource Save-As Feature** | **New Feature** | No streamlined method for creating additional presets with named copies of linked resources.            | Added a "Save As" button and menu option to save linked resources with new names. Implemented a dialog that provides a guided workflow for naming and saving linked resources along with Tool Presets. |

---

#### **Key Changes**

- **Icon Picker Update**:
   - Added a new `icon_tool_preset` boolean property to dynamically adjust the icon picker's size in the Tool Preset Editor.
   - Enlarged and centered the icon picker for better usability on HDPI screens.

- **Tool Preset Information Table**:
   - Introduced an information table that displays both the saved and active states of resources linked to Tool Presets.
   - This provides users with clear insights into linked resource configurations, enhancing editing and creation workflows.

- **Resource Reloading Options**:
   - Consolidated the Tool Preset Editor’s resource reloading options into a collapsible "Resource Reloading" frame using a GTK expander widget.
   - Added tooltips to clarify the purpose of each option, improving usability and reducing interface clutter.

- **Linked Resource Saving Options**:
   - Added a collapsible "Linked Resource Saving" frame for managing linked resource options when saving Tool Presets.
   - Ensures streamlined handling of linked resources for both new and existing presets.

- **Save-As Feature for Linked Resources**:
   - Introduced a "Save As" button and menu option for saving linked resources with new names.
   - Created an interactive dialog to guide users through naming linked resources and saving Tool Presets.

---

### **Benefits**

- **Improved Usability**: The enlarged icon picker and structured layout of the Tool Preset Editor enhance visual feedback and accessibility.
- **Streamlined Workflows**: New options for managing linked resources simplify the process of creating and editing Tool Presets.
- **Reduced Interface Clutter**: Collapsible frames and grouped options reduce visual noise, ensuring an organized and compact interface.
- **Enhanced Discoverability**: Tooltips and guided dialogs improve feature discoverability, particularly for new users.

