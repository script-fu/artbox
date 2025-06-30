---
type: docs
url: "hub/feature-test/folder/Warp-Tool"
---

# Objective

Enable warping functionality for Layer Groups in Artbox to support a flexible design process, allowing artists to dynamically adjust work within highly structured files containing hundreds of layers.

## Related Links

- Youtube [Demo](https://youtu.be/nUbQFMhGr1s)

## Design Revisions

{{< cards >}}
  {{< card link="#warp-layer-groups" title="Warp Layer Groups" subtitle="Transform entire layer groups together" icon="collection" >}}
  {{< card link="#group-masks-warping" title="Group Masks Warping" subtitle="Control mask transformation behavior" icon="eye" >}}
  {{< card link="#configurable-warp-margin" title="Configurable Warp Margin" subtitle="Prevent clipping during transformation" icon="arrows-expand" >}}
  {{< card link="#tool-restart-usable-state" title="Tool Restart in Usable State" subtitle="Always start in a functional mode" icon="refresh" >}}
  {{< card link="#last-undo-notification" title="Last Undo Notification" subtitle="Alert when reaching undo limit" icon="bell" >}}
  {{< card link="#layer-change-notification" title="Layer Change Notification" subtitle="Prevent mid-warp layer switching" icon="exclamation" >}}
  {{< card link="#display-change-auto-commit" title="Display Change Auto-Commit" subtitle="Maintain consistency across displays" icon="desktop-computer" >}}
  {{< card link="#warp-item-validation" title="Warp Item Validation" subtitle="Validate layer compatibility" icon="check-circle" >}}
{{< /cards >}}

---

<div class="feature-section" id="warp-layer-groups">

## Warp Layer Groups

**Current State**: Layers can only be warped individually.

**Issue**: Warping a group of layers together is unsupported, limiting transformations on complex structures.

**Solution**: Introduced the ability to warp entire layer groups, including their masks.

**Implementation**: Introduced `WarpGroup` structure to handle warping across multiple items within a layer group. Enhanced functions like `gimp_warp_tool_group_commit` and `initialize_warp_tool` to process Layer Groups, including bounding box calculations and grouped warping.

</div>

<div class="feature-section" id="group-masks-warping">

## Group Masks Warping

**Current State**: New Feature.

**Issue**: Masks don't always need to be warped, requiring flexibility.

**Solution**: Added a Warp Transform option to enable or disable group mask warping.

**Implementation**: Added a toggle (`PROP_GROUP_WARP_GROUP_MASKS`) in `gimp_warp_options_gui` to control mask warping within groups. This boolean setting allows users to include group masks in the warp transformations, depending on artistic needs.

</div>

<div class="feature-section" id="configurable-warp-margin">

## Configurable Warp Margin

**Current State**: Layers can exceed defined boundaries during transformations, leading to clipping or distortion.

**Issue**: Warping beyond layer boundaries results in inconsistent or incomplete transformations.

**Solution**: Added a configurable `Margin` slider for group expansion to accommodate boundary extensions.

**Implementation**: Implemented the `PROP_GROUP_MARGIN` setting for customizable margins around layer groups. This margin prevents content clipping during warp transformations by providing a configurable buffer, adjustable from 16 to 2048 pixels.

</div>

<div class="feature-section" id="tool-restart-usable-state">

## Tool Restart in Usable State

**Current State**: Tool can restart in any mode, including `Erase` and `Smooth`, even if no content is available to warp.

**Issue**: Starting in `Erase` or `Smooth` mode with no warp content to modify creates a usability issue.

**Solution**: Tool now restarts in `Move` mode if the previous action leaves it in an unusable state.

**Implementation**: Ensures the tool restarts in `Move` mode if previous actions would otherwise leave it in `Erase` or `Smooth` modes, which require existing content to function.

</div>

<div class="feature-section" id="last-undo-notification">

## Last Undo Notification

**Current State**: Tool doesn't indicate when the last available undo is reached.

**Issue**: Users may attempt further undo actions without realizing they've reached the limit, causing confusion.

**Solution**: Added a status message to notify users when they've reached the last undo, helping them manage next steps carefully.

**Implementation**: Provides a status message alerting users when they are at the final undo step, guiding them to proceed carefully.

</div>

<div class="feature-section" id="layer-change-notification">

## Layer Change Notification

**Current State**: Users can switch layers while performing a group warp.

**Issue**: Switching layers mid-warp may cause data inconsistencies and unexpected visual results in the warped layer.

**Solution**: Added a notification that prompts users to commit the current warp before switching layers and reselects the warp layer.

**Implementation**: In group warping mode, the tool prompts users to commit the current warp before switching layers. The warp layer is automatically reselected, ensuring that users complete changes on the active layer before proceeding with other edits.

</div>

<div class="feature-section" id="display-change-auto-commit">

## Display Change Auto-Commit

**Current State**: Users can switch displays mid-warp without committing, leading to potential data loss or visual issues.

**Issue**: Changing displays mid-warp can prevent the warp tool's indicator circle from drawing correctly on either display.

**Solution**: Auto-commit on display switch ensures correct behavior and prepares the tool for immediate use on the new display.

**Implementation**: When the user changes displays mid-warp, the tool automatically commits the current warp. This adjustment maintains data consistency across displays and prepares the tool for immediate use on the new display.

</div>

<div class="feature-section" id="warp-item-validation">

## Warp Item Validation

**Current State**: New Feature.

**Issue**: Warping incompatible items, locked layers, or empty content may cause errors or slowdown.

**Solution**: Added `is_valid_warp_item` to validate items in groups, checking for locked, empty, or out-of-bounds layers.

**Implementation**: Introduced `is_valid_warp_item` to validate items within groups for compatibility with the warp process. This function checks if an item is in `tmp_expand_layers`, is content-locked, has a valid bounding box, and intersects with the warped area. Items are further examined using an enhanced `gimp_pickable_auto_shrink` function, allowing classification of items as empty, uniform, or containing non-black pixels to optimize warp applicability.

</div>

## Known Issues

- **Undo/Redo Limitations**: Undo then Redo may fail due to an unknown issue with Layer Group mask handling. It's advised to save before warping, and use autosave and incremental saving.
- **Experimental Freeze Feature**: Freezing the Layer Stack container to improve update speed and restrict GUI interaction causes erratic behavior in the Layer Stack post-warp. This experimental feature can be enabled via a code flag. Layer Group warping requires further testing and code review due to the complexity of the operation.
