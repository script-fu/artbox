---
type: docs
url: "hub/feature-test/folder/Selection-Display"
---

# Objective

Improve the quality of the painting experience in Artbox by enhancing the active selection behavior.

## Design Revisions

| **Revision**  | **Current Design**  | **Issues**  | **Changes** |
|--------------------------------------------|---------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------|-----------------------------------------------------------|
| **1. Selection Mask Highlighting** | Rectangle selection highlighting is on a few tools, and is not global | Knowing if there is an active selection can be an issue. Working without selection borders becomes difficult. Changing tools loses the selection highlighting. | Draw a shaded overlay that masks out unselected areas. Additional preference options for the shade alpha and colour. Additional View option 'Show Selection Highlight' to toggle with a shortcut to quickly turn off and on. |
| **2. Select All Highlighting** | No clear indication of a `Select All` state | Knowing if there is an active select all can be an issue. | Draw a shaded frame on the canvas padding that indicates select all. |
| **3. Selection Borders**   | New Feature | No way to adjust the thickness or harshness of selection borders | Added preferences to adjust the selection border |
| **4. Selection Status**   | New Feature | When 'Show Selection', and in Artbox 'Show Selection Highlight' are off, no indiction of an active selection is given | Added a Status Bar label that indicates when there is an 'invisible' selection |

### **Benefits**

These updates allow the user to work without selection borders, or with softer selection borders. With accurate selection area shading, knowing what content is editable becomes more intuitive.

When the user wants to paint a selection area without any obscuring but visible indiction on the image, then a Status Bar indiction is given.

**Edit > Preferences > Image Windows > Selection Highlighting**
**View > Show Selection Highlight**

Video on [YouTube](https://youtu.be/RG3rOhjXXW0)
