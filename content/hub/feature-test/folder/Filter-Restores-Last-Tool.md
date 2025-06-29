---
type: docs
url: "hub/feature-test/folder/Filter-Restores-Last-Tool"
---

# Objective

Removes a long-standing GUI issue.

## Key Concepts and Definitions

- **Filter**: A plug-in that processes pixels in a drawable, Hue, Blur etc.
- **Tool Palette**: The grid of tool buttons, Move Tool, Paintbrush Tool ect.

## Design Revisions

| **Revision**  | **Current Design**  | **Issues**  | **Changes** |
|--------------------------------------------|---------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------|-----------------------------------------------------------|
| **1. Restore the previous tool after using a filter** | The filter is the active tool | Confusing to the user to deselect the active tool when a filter is used, and to keep the filter as the active tool | Restore the previous tool when a filter dialog is closed |

### Changes

- **Restore Previous Tool After Filter Use**:
  - Added code to retrieve the previous tool from the context.
  - After a filter dialog closes (whether committed or canceled), the previous tool is restored using `gimp_context_set_tool`.

### **Benefits**

- Ensures the user's previous tool is restored after using a filter, providing a more intuitive and seamless experience in the tool palette.
