---
type: docs
---

# Objective

Improve the Color Picker Tool

## Design Revisions

| **Revision**  | **Current Design**  | **Issues**  | **Changes** |
|--------------------------------------------|---------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------|-----------------------------------------------------------|
| **1. Alt Key Toggles Sample Merged** | New Feature | Never know what state the sample option was left in | Whilst `Alt` is pressed toggle the Sample Merged state |

### **Benefits**

The user can set the default state for the Sample Merged option in the Color Picker Tool as needed, and it will stay in that state. For example, when using `Ctrl` to pick while painting (which follows the current state of the Color Picker Tool), Sample Merged is turned off by default. If you want to sample merged, select the Color Picker Tool and hold Alt while picking. This method removes the unpredictable changes in the sampling method of the picker tool.
