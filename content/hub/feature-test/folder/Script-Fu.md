---
type: docs
---

# Objective

Extend Script-Fu to include additional functions that help the user.

## Key Concepts and Definitions

- **Script-Fu**: A scripting language based on Scheme

## Additional Procedures

| **Command** | **Purpose** |
| --- | --- |
| (gimp-context-get-display) | Get the active display ID |
| (gimp-context-eraser-toggle) | Toggle the tool to the eraser. |
| (gimp-items-set-visible) | Set the visibility of a vector list of items |

### Changes

1. **New Script-Fu Functions**:
   - `(gimp-context-get-display)`: Retrieves the active display ID. This ID can then be used with other display-related functions like `(gimp-display-present display-id)`.
   - `(gimp-context-eraser-toggle)`: Toggles the active tool between the eraser and the previously active tool.
   - `(gimp-items-set-visible)`: Allows setting the visibility of a vector list of items in bulk. This can help streamline visibility management for layers, paths, or other drawable items.

### **Benefits**

- These additional functions enhance the flexibility of Script-Fu, enabling users to toggle between tools, manage visibility across multiple items, and integrate display information into their scripts, leading to more powerful automation and customization.
