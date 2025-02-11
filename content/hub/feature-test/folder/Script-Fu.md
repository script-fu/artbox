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
| (gimp-context-eraser-toggle) | Toggle the active tool to the eraser. |
| (gimp-context-eraser-paintbrush-toggle) | Toggle the active tool to the eraser and always return to the paintbrush |
| (gimp-context-get-eraser-active ) | Returns true if the Eraser Tool is active |
| (gimp-items-set-visible) | Set the visibility of a vector list of items |

### Changes

- **New Script-Fu Functions**:
   - `(gimp-context-get-display)`: Retrieves the active display ID. This ID can then be used with other display-related functions like `(gimp-display-present display-id)`.
   - `(gimp-context-eraser-toggle)`: Toggles the active tool between the eraser and the previously active tool.
   - `(gimp-context-eraser-paintbrush-toggle)`: Toggles the active tool between the eraser and the paintbrush tool.
   - `(gimp-context-get-eraser-active)`: Returns 1 if the Eraser Tool is active or 0.
   - `(gimp-items-set-visible)`: Allows setting the visibility of a vector list of items in bulk. This can help streamline visibility management for layers, paths, or other drawable items.

### **Benefits**

- These additional functions enhance the flexibility of Script-Fu, enabling users to toggle between tools, manage visibility across multiple items, and integrate display information into their scripts, leading to more powerful automation and customization.
