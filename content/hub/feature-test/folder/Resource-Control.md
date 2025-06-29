---
type: docs
url: "hub/feature-test/folder/Resource-Control"
---

# Objective

Improve the usability and data saving of resources and Tool Presets in Artbox.

## Revised Preferences

- Preferences >
  - Folders > Show the Copy Resource Location menu item
  - Folders > Save resource changes on exit
  - Interface > Resource Filtering > Enable Resource Filtering and Tagging

## Design Revisions

| **Revision**  | **Current Design**  | **Issues**  | **Changes** |
|--------------------------------------------|---------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------|-----------------------------------------------------------|
| **1. Deactivate automatic resource saving** | Saves are done when GIMP exits | Tweaks to resources in session can corrupt carefully set up tools with unwanted changes. | A Preference to 'Save resource changes on exit'
| **2. Save specific resource changes immediately**   | Saves are done when GIMP exits | Changes to resources are lost if GIMP crashes or exits with a crash.  | Save immediately when clicked |
| **3. Save As**   | Saves are done with default naming | The name of the saved resource is not the same as the filename, this is confusing.  | Save immediately with a naming option, Save As...|
| **4. Save All** | If saves are done by the user on demand, as described in (2) or (3), a new issue arises| Changes to resources may be forgotten during the session. Saving one by one is error prone and time consuming | Add 'Save all the active tool assets' button and a 'Save all changes' button on the Preset Editor  |
| **5. Simpler Menu** | Menu item 'Copy Resource Location' exists in several menus | Not used by most users, creates menu clutter |  A Preference to 'Show Copy Resource Location menu item'  |
| **6. Button Bar and Menu Revised** | See menu items and Button Bar GUI in GIMP | Confusing item placement, Button Bar GUI out of step with updates from (1-5) |  Apply a consistent menu item position, and arrange Button Bars to support the changes  |
| **7. Edit Brush deals with Parametric and Image types** | See Brushes Menu items | Confusion over brush types |  Double clicking an image type opens the image for editing, Double clicking a parametric type opens the Brush Editor |
| **8. Inform the user about locked resources** | Folder locked resources can not be edited | User confusion | An informative message is displayed in the Brush Editor if the resource is locked |
| **9. Copy and Paste as New Brush** | New Feature | Create a brush from the active drawable | Added to the Brushes Menu via a Script-Fu plug-in |
| **10. Tool Preset Name in Tool Options Title** | New Feature | See the active Tool Preset name requires the Tool Preset Editor to be open or the Tool Preset selector to be in list mode | Added the active Tool Preset name after the Tool name in the Tool Options title. Tool Name | Tool Preset Name |
| **11. Preferences Folder Options** | New Feature | Folders have to be manually added or removed per resource | Added a GUI to add, deactivate, or remove folder paths to a set of resources, allowing quick control over active resources |
| **12. Resource Filtering** | New Feature | User never uses filtering and it takes up GUI space and adds complexity | Added Preference option, Interface > Resource Filtering > Enable Resource Filtering and Tagging |
| **13. Icon View Preview** | Themes button appears in Icon view grid modes to toggle background colour of preview | Adds GUI clutter that also appears in the Tool Presets view, user sets once, button hangs around forever. | Hardcode the previews to use the theme background colour and hide the toggle button. |

### Changes

- **Resource Saving Preferences:**
   - Introduced a new preference to toggle automatic resource saving on exit, preventing unwanted overwriting of user-set Tool Options during a session. This allows users to disable automatic saving and manually save specific changes when needed.

- **Immediate Resource Saving:**
   - Added functionality to save specific resource changes immediately upon request, ensuring that any modifications are persisted, even if the session ends unexpectedly. This avoids data loss in case of a crash.

- **Save As:**
   - A 'Save As' feature was added, allowing users to name and save resources with custom filenames, enhancing clarity and preventing confusion between resource names and file names.

- **Save All:**
   - Introduced a 'Save All' option to the Preset Editor, enabling users to save all active changes across tool presets, brushes, palettes, and other resources, reducing the need for manual per-resource saves.

- **Simplified Menus and Button Bar:**
   - Cleaned up the interface by providing an option to hide the 'Copy Resource Location' menu item, which was seldom used, thereby reducing menu clutter.
   - Rearranged the Button Bar to reflect the new saving behaviors and align with the revised menus for consistency.

- **Brush Editor Enhancements:**
   - Adjusted the behavior for brush types so that double-clicking on image-type brushes opens the image for editing, while double-clicking on parametric brushes opens the Brush Editor. This resolves the confusion around brush types.

- **Locked Resource Notification:**
   - When a resource is locked (due to folder permissions), the user will now receive an informative message in the Brush Editor, improving clarity on why the resource cannot be modified.

- **Create New Brush from Drawable:**
   - Added the ability to copy and paste a drawable as a new brush via a Script-Fu plug-in, accessible from the Brushes Menu.

- **Save Active Tool Assets:**
   - Introduced a 'Save All Active Tool Assets' feature, allowing users to save all the active tool assets (brush, gradient, palette, dynamics) in a session for easier resource management.

- **Tool Preset Name in Tool Options Title:**
   - Added the active Tool Preset name after the Tool name in the Tool Options title. Tool Name | Tool Preset Name.  We can see which Tool Preset is active from the Tool Options Title.

- **Preferences Folder Options:**
   - Added a GUI to add, deactivate, or remove folder paths for a sets of resources, allowing quick control over in session resources.

- **Resource Filtering:**
   - Added Preference option, Interface > Resource Filtering > Enable Resource Filtering and Tagging. This allows the user who does not use the filtering to have a simpler GUI.

- **Less clutter:**
   - Hardcode the icon view previews to use the theme background colour and hide the Themes toggle button.

### **Benefits**

These changes aim to provide better control over resources and presets, allowing users to manage their assets more intuitively and prevent unintended modifications.
