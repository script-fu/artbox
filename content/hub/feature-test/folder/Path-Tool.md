---
type: docs
---

# Objective

Enhance path editing, snapping, and visibility features while refining path commitment behavior to prevent unintentional selections.

## Design Revisions

| **Revision**                   | **Current Design**                                    | **Issues**                                                        | **Changes**                                            |
|--------------------------------|-------------------------------------------------------|-------------------------------------------------------------------|--------------------------------------------------------|
| **1. Path Snap Distance**       | Snapping uses a single distance for grid, guides, and paths. | Users can't adjust snapping precision separately for paths.       | Introduced an independent `Active Paths` snap preference option. |
| **2. Path Visibility Control**   | Created paths aren't visible by default.             | Users need to manually enable visibility for new paths.           | Added visibility control for paths at creation via a new `Visible` property. |
| **3. Handle Locking**            | No lock handles option for path editing.    | Limits, making certain edits awkward.     | Added a `lock_handles` property to lock handles during editing. |
| **4. Enhanced Movement Controls** | Movement lacks refined state controls for duplicating and snapping. | Limited control and feedback for path manipulation workflows. | Added automatic `Move` mode upon path duplication, intuitive handle and curve point movement, and a "Finish Edit Mode" button. |
| **5. Enter Key Path Commitment**  | Enter previously selected enclosed area on path commitment. | Selection behavior was often distracting and unwanted.            | Updated Enter to commit path edits without selecting enclosed areas. |
| **6. Path Rendering**   | New Feature | No way to adjust the thickness or harshness of a Path | Added preferences to adjust the Path Rendering |
| **7. Path Content Lock**   | New Feature | Path content lock and Position lock are identical in function, path is fully locked | Content lock now allows the user to use the `Move` mode and move the path, anchors or control points. |

### Changes

1. **Path Snap Distance**:
   - Edit -> Preferences -> Canvas Interaction -> Snapping -> Snapping Distance -> Active Path

2. **Path Visibility Control**:
   - Added a "Visible Path" checkbox in the Path Tool options GUI for quick user control over path visibility.

3. **Handle Locking**:
   - Added a "Lock Handles" option in the GUI, allowing users to easily enable handle locking.

4. **Enhanced Movement Controls**:
   - Automatically switches to `Move` mode after duplicating a path, simplifying workflow.
   - Updated path handle and curve point interactions for a more intuitive editing experience.
   - Increase the size of the handles for HDPI.
   - Added a "End Edit Mode" button in vector tool options, allowing users to quickly exit edit mode, to start a new path.

5. **Enter Key Path Commitment**:
   - Updated the `Enter` key functionality to commit path edits without selecting the enclosed area, preventing unintended selections that could disrupt workflow, especially with linear paths.

6. **Edit > Preferences > Image Windows > Path Rendering**
   - Adjust the alpha and thickness of path lines.
7. **Content Locking**:
   - Content lock now allows the user to use the `Move` mode and move the path, anchors or control points.

### **Benefits**

- **Improved Snap Control**: Users can adjust snap distances independently for paths, providing more precise control based on element type (e.g., paths vs. grids).
- **Enhanced Workflow with Auto-Visibility**: Paths are automatically visible upon creation, improving user feedback and reducing manual toggling.
- **Streamlined Movement & Editing**: Movement and editing controls are more refined, with automatic `Move` mode for path duplicates, handle locking options, and a quick exit button from edit mode.
- **Refined Path Commitment**: The Enter key now only commits path changes without selecting enclosed areas, reducing distractions and providing a smoother workflow for linear and complex paths.
- **Adjustable Rendering**: See the work behind the path.
- **Lock Content** to restrict a specific path to movement only. This stops the user accidentally adding more strokes or points to a path, which is very easy to do in Design and Edit modes.
