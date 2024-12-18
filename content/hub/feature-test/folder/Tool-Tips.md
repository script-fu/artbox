---
type: docs
---

# Objective

Improve the quality of the user interface experience by optionally deactivating distracting tool tips.

## Design Revisions

| **Revision**             | **Current Design**                                                                                         | **Issues**                                                                                          | **Changes**                                                                                           |
|--------------------------|------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------|
| **1. Configurable Tooltips** | Tooltips cannot be turned off                                                                           | Users cannot stop distracting tips from flickering on and off                                        | Introduced a new Preferences option, `Show tool tips`, allowing users to toggle some tooltips on or off. |

### Changes

- **Configurable Tooltip Property**:
   - Added a new `show_tool_tips` property to the `GimpGuiConfig` structure, making tooltip display configurable through the codebase.

- **Tooltip Preference Integration**:
   - Integrated the tooltip preference under `Preferences -> Interface -> Help System -> General -> Show tool tips`, allowing users to toggle tooltip visibility easily within the UI.

### **Benefits**

- The addition of the `show_tool_tips` option enhances user control over the interface, reducing UI clutter for users who prefer minimal tool guidance, while retaining tooltip functionality for those who rely on detailed tool descriptions. Though primarily a workaround to reduce tooltip distractions, a more granular solution could be implemented for further customization.


