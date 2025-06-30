---
type: docs
url: "hub/feature-test/folder/Path-Tool"
---

# Objective

Enhance path editing, snapping, and visibility features while refining path commitment behavior to prevent unintentional selections.

## Design Revisions

{{< cards >}}
  {{< card link="#path-snap-distance" title="Path Snap Distance" subtitle="Independent snapping precision for paths" icon="cursor-click" >}}
  {{< card link="#path-visibility-control" title="Path Visibility Control" subtitle="Automatic visibility for new paths" icon="eye" >}}
  {{< card link="#handle-locking" title="Handle Locking" subtitle="Lock handles during path editing" icon="lock-closed" >}}
  {{< card link="#enhanced-movement-controls" title="Enhanced Movement Controls" subtitle="Refined path manipulation workflow" icon="hand" >}}
  {{< card link="#enter-key-path-commitment" title="Enter Key Path Commitment" subtitle="Commit paths without unwanted selection" icon="check" >}}
  {{< card link="#path-rendering" title="Path Rendering" subtitle="Adjustable path appearance" icon="color-swatch" >}}
  {{< card link="#path-content-lock" title="Path Content Lock" subtitle="Content lock with movement flexibility" icon="shield-check" >}}
{{< /cards >}}

### Detailed Changes

<div class="feature-section" id="path-snap-distance">

#### 1. Path Snap Distance

- **Current Design**: Snapping uses a single distance for grid, guides, and paths.
- **Issues**: Users can't adjust snapping precision separately for paths.
- **Changes**: Introduced an independent `Active Paths` snap preference option.
- **How to Use**: Edit → Preferences → Canvas Interaction → Snapping → Snapping Distance → Active Path
- **Benefits**: Users can adjust snap distances independently for paths, providing more precise control based on element type (e.g., paths vs. grids).

</div>

<div class="feature-section" id="path-visibility-control">

#### 2. Path Visibility Control

- **Current Design**: Created paths aren't visible by default.
- **Issues**: Users need to manually enable visibility for new paths.
- **Changes**: Added visibility control for paths at creation via a new `Visible` property.
- **How to Use**: Added a "Visible Path" checkbox in the Path Tool options GUI for quick user control over path visibility.
- **Benefits**: Paths are automatically visible upon creation, improving user feedback and reducing manual toggling.

</div>

<div class="feature-section" id="handle-locking">

#### 3. Handle Locking

- **Current Design**: No lock handles option for path editing.
- **Issues**: Limits flexibility, making certain edits awkward.
- **Changes**: Added a `lock_handles` property to lock handles during editing.
- **How to Use**: Added a "Lock Handles" option in the GUI, allowing users to easily enable handle locking.
- **Benefits**: Provides better control for precise path editing by preventing accidental handle movement.

</div>

<div class="feature-section" id="enhanced-movement-controls">

#### 4. Enhanced Movement Controls

- **Current Design**: Movement lacks refined state controls for duplicating and snapping.
- **Issues**: Limited control and feedback for path manipulation workflows.
- **Changes**: Added automatic `Move` mode upon path duplication, intuitive handle and curve point movement, and a "Finish Edit Mode" button.
- **How to Use**: 
  - Automatically switches to `Move` mode after duplicating a path
  - Updated path handle and curve point interactions for more intuitive editing
  - Increased handle size for HDPI displays
  - Added "End Edit Mode" button in vector tool options for quick exit to start new paths
- **Benefits**: Streamlined movement and editing controls with automatic `Move` mode for path duplicates, handle locking options, and quick exit from edit mode.

</div>

<div class="feature-section" id="enter-key-path-commitment">

#### 5. Enter Key Path Commitment

- **Current Design**: Enter previously selected enclosed area on path commitment.
- **Issues**: Selection behavior was often distracting and unwanted.
- **Changes**: Updated Enter to commit path edits without selecting enclosed areas.
- **How to Use**: Simply press Enter to commit path edits without creating a selection
- **Benefits**: The Enter key now only commits path changes without selecting enclosed areas, reducing distractions and providing a smoother workflow for linear and complex paths.

</div>

<div class="feature-section" id="path-rendering">

#### 6. Path Rendering

- **Current Design**: New Feature
- **Issues**: No way to adjust the thickness or harshness of a Path.
- **Changes**: Added preferences to adjust the Path Rendering.
- **How to Use**: Edit → Preferences → Image Windows → Path Rendering to adjust alpha and thickness of path lines
- **Benefits**: Adjustable rendering lets you see the work behind the path and customize visibility for your workflow.

</div>

<div class="feature-section" id="path-content-lock">

#### 7. Path Content Lock

- **Current Design**: New Feature
- **Issues**: Path content lock and Position lock are identical in function, path is fully locked.
- **Changes**: Content lock now allows the user to use the `Move` mode and move the path, anchors or control points.
- **How to Use**: Content lock now allows using `Move` mode to move paths, anchors, or control points
- **Benefits**: Lock content to restrict a specific path to movement only. This prevents accidentally adding more strokes or points to a path, which is very easy to do in Design and Edit modes.

</div>
