---

type: docs

---

# Objective

Enable warping functionality for Layer Groups in Artbox to support a flexible design process, allowing artists to dynamically adjust work within highly structured files containing hundreds of layers.

## Related Links

- Youtube [Demo](https://youtu.be/nUbQFMhGr1s)

## Design Revisions

| **Revision**                   | **Current Design**                                                                                  | **Issues**                                                                                             | **Changes**                                                                                                         |
|--------------------------------|----------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------|
| **1. Warp Layer Groups**       | Layers can only be warped individually.                                                            | Warping a group of layers together is unsupported, limiting transformations on complex structures.     | Introduced the ability to warp entire layer groups, including their masks.                                          |
| **2. Group Masks Warping**     | New Feature                                                                                         | Masks don’t always need to be warped, requiring flexibility.                                           | Added a Warp Transform option to enable or disable group mask warping.                                               |
| **3. Configurable Warp Margin**| Layers can exceed defined boundaries during transformations, leading to clipping or distortion.    | Warping beyond layer boundaries results in inconsistent or incomplete transformations.                 | Added a configurable `Margin` slider for group expansion to accommodate boundary extensions.                        |
| **4. Tool Restart in Usable State** | Tool can restart in any mode, including `Erase` and `Smooth`, even if no content is available to warp. | Starting in `Erase` or `Smooth` mode with no warp content to modify creates a usability issue.        | Tool now restarts in `Move` mode if the previous action leaves it in an unusable state.                             |
| **5. Last Undo Notification**       | Tool doesn’t indicate when the last available undo is reached.                                      | Users may attempt further undo actions without realizing they’ve reached the limit, causing confusion. | Added a status message to notify users when they’ve reached the last undo, helping them manage next steps carefully. |
| **6. Layer Change Notification**    | Users can switch layers while performing a group warp.                                          | Switching layers mid-warp may cause data inconsistencies and unexpected visual results in the warped layer. | Added a notification that prompts users to commit the current warp before switching layers and reselects the warp layer. |
| **7. Display Change Auto-Commit**   | Users can switch displays mid-warp without committing, leading to potential data loss or visual issues. | Changing displays mid-warp can prevent the warp tool’s indicator circle from drawing correctly on either display. | Auto-commit on display switch ensures correct behavior and prepares the tool for immediate use on the new display.   |
| **8. Warp Item Validation**         | New Feature                                                                                       | Warping incompatible items, locked layers, or empty content may cause errors or slowdown.              | Added `is_valid_warp_item` to validate items in groups, checking for locked, empty, or out-of-bounds layers.       |

### Changes

- **Warp Layer Groups**:
   - Introduced `WarpGroup` structure to handle warping across multiple items within a layer group.
   - Enhanced functions like `gimp_warp_tool_group_commit` and `initialize_warp_tool` to process Layer Groups, including bounding box calculations and grouped warping.

- **Warp Group Masks**:
   - Added a toggle (`PROP_GROUP_WARP_GROUP_MASKS`) in `gimp_warp_options_gui` to control mask warping within groups.
   - This boolean setting allows users to include group masks in the warp transformations, depending on artistic needs.

- **Configurable Warp Margin**:
   - Implemented the `PROP_GROUP_MARGIN` setting for customizable margins around layer groups.
   - This margin prevents content clipping during warp transformations by providing a configurable buffer, adjustable from 16 to 2048 pixels.

- **Tool Restart in Usable State**:
   - Ensures the tool restarts in `Move` mode if previous actions would otherwise leave it in `Erase` or `Smooth` modes, which require existing content to function.

- **Last Undo Notification**:
   - Provides a status message alerting users when they are at the final undo step, guiding them to proceed carefully.

- **Layer Change Notification**:
   - In group warping mode, the tool prompts users to commit the current warp before switching layers.
   - The warp layer is automatically reselected, ensuring that users complete changes on the active layer before proceeding with other edits.

- **Display Change Auto-Commit**:
   - When the user changes displays mid-warp, the tool automatically commits the current warp.
   - This adjustment maintains data consistency across displays and prepares the tool for immediate use on the new display.

- **Warp Item Validation**:
   - Introduced `is_valid_warp_item` to validate items within groups for compatibility with the warp process.
   - This function checks if an item is in `tmp_expand_layers`, is content-locked, has a valid bounding box, and intersects with the warped area.
   - Items are further examined using an enhanced `gimp_pickable_auto_shrink` function, allowing classification of items as empty, uniform, or containing non-black pixels to optimize warp applicability.

### **Benefits**

These updates provide extended control over complex layer group warping, improve visual feedback, and prevent boundary clipping during transformations. The ability to warp group masks improves consistency for multi-layer transformations, while the margin setting allows for flexibility with expanded areas within the canvas. Usability improvements—such as automatic commits on display switches, notifications for undo limits, and compatibility validation for warp items—enhance workflow efficiency and user experience. Artists who work in a non-destructive, layered format can now refine their work at any stage using the Warp Transform on nested Layer Groups.

### Known Issues

- **Undo/Redo Limitations**: Undo then Redo may fail due to an unknown issue with Layer Group mask handling. It’s advised to save before warping, and use autosave and incremental saving.
- **Experimental Freeze Feature**: Freezing the Layer Stack container to improve update speed and restrict GUI interaction causes erratic behavior in the Layer Stack post-warp. This experimental feature can be enabled via a code flag. Layer Group warping requires further testing and code review due to the complexity of the operation.

