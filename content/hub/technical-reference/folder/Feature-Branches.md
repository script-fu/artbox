---
type: docs
url: "hub/technical-reference/folder/Feature-Branches"
---

# Feature Branches

Feature branches implement specific Artbox functionality and enhancements built on top of the convert branch foundation.

## Branch Overview

{{< cards >}}
  {{< card link="#feature-paintbrush-high-quality-force" title="feature-paintbrush-high-quality-force" subtitle="High-quality paintbrush rendering enforcement" >}}
  {{< card link="#feature-presets-restore" title="feature-presets-restore" subtitle="Tool preset restoration functionality" >}}
  {{< card link="#feature-toolbox" title="feature-toolbox" subtitle="Updated toolbox interface and behavior" >}}
  {{< card link="#feature-painttool" title="feature-painttool" subtitle="Paint tool functionality" >}}
  {{< card link="#feature-resource-control" title="feature-resource-control" subtitle="Resource management with save-as functionality (74 files)" >}}
  {{< card link="#feature-dynamic-output" title="feature-dynamic-output" subtitle="Angular dynamics with multiplier modes (388 lines)" >}}
  {{< card link="#feature-selection" title="feature-selection" subtitle="Selection tools and behavior" >}}
  {{< card link="#feature-transform-tool" title="feature-transform-tool" subtitle="Updated transformation tools" >}}
  {{< card link="#feature-filter-restores-last-tool" title="feature-filter-restores-last-tool" subtitle="Filter operations restore previous tool" >}}
  {{< card link="#feature-script-fu-plugins" title="feature-script-fu-plugins" subtitle="20 custom plugins with workflow automation (9,008 lines)" >}}
  {{< card link="#feature-dynamic-brush-spacing" title="feature-dynamic-brush-spacing" subtitle="Dynamic brush spacing control" >}}
  {{< card link="#feature-motion-buffer" title="feature-motion-buffer" subtitle="Motion buffer for smooth strokes" >}}
  {{< card link="#feature-smooth-stroke" title="feature-smooth-stroke" subtitle="Stroke smoothing" >}}
  {{< card link="#feature-eraser" title="feature-eraser" subtitle="Enhanced eraser functionality" >}}
  {{< card link="#feature-snapping" title="feature-snapping" subtitle="Enhanced snapping functionality" >}}
  {{< card link="#feature-path-editing" title="feature-path-editing" subtitle="Path editing tools" >}}
  {{< card link="#feature-colour-picker" title="feature-colour-picker" subtitle="Color picker functionality" >}}
  {{< card link="#feature-layer-pop-up-menu" title="feature-layer-pop-up-menu" subtitle="Layer context menu enhancements" >}}
  {{< card link="#feature-supress-warning-messages" title="feature-supress-warning-messages" subtitle="Warning message suppression" >}}
  {{< card link="#feature-simple-sliders" title="feature-simple-sliders" subtitle="Simplified slider interface" >}}
  {{< card link="#feature-warp-update" title="feature-warp-update" subtitle="Warp tool enhancements" >}}
  {{< card link="#feature-gui-size-tweaks" title="feature-gui-size-tweaks" subtitle="GUI size adjustments" >}}
  {{< card link="#feature-paintbrush-slider-tool-tips" title="feature-paintbrush-slider-tool-tips" subtitle="Paintbrush slider tooltips" >}}
  {{< card link="#feature-additional-script-fu" title="feature-additional-script-fu" subtitle="Additional Script-Fu functionality" >}}
  {{< card link="#feature-selection-highlight" title="feature-selection-highlight" subtitle="Selection highlighting enhancements" >}}
  {{< card link="#feature-gfig" title="feature-gfig" subtitle="GFig plugin improvements" >}}
  {{< card link="#feature-status-bar" title="feature-status-bar" subtitle="Status bar enhancements" >}}
  {{< card link="#feature-fullscreen-is-fullscreen" title="feature-fullscreen-is-fullscreen" subtitle="True fullscreen mode" >}}
  {{< card link="#feature-style-settings" title="feature-style-settings" subtitle="Style and theme settings" >}}
  {{< card link="#feature-max-brush-size" title="feature-max-brush-size" subtitle="Maximum brush size adjustments" >}}
  {{< card link="#feature-duplicate-layer-and-clear" title="feature-duplicate-layer-and-clear" subtitle="Layer duplication and clearing" >}}
  {{< card link="#feature-data-factory-filter" title="feature-data-factory-filter" subtitle="Data factory filtering" >}}
  {{< card link="#feature-jitter" title="feature-jitter" subtitle="Brush jitter enhancements" >}}
  {{< card link="#feature-recent-layer-mode-group" title="feature-recent-layer-mode-group" subtitle="Recent layer mode grouping" >}}
{{< /cards >}}

---

<div class="feature-section" id="feature-paintbrush-high-quality-force">

## feature-paintbrush-high-quality-force

**Purpose**: Memory safety and high-quality paintbrush rendering with improved buffer allocation and integer overflow protection.

**Role**: Improvement to paintbrush rendering pipeline that adds safety checks while enabling high-quality force parameters for paint output.

**Files Modified** (2 files, 78 insertions, 50 deletions):
- `app/core/gimptempbuf.c` (97 lines modified): Enhanced buffer allocation with overflow protection and improved memory safety
- `app/paint/gimpbrushcore-loops.cc` (31 lines modified): Updated brush rendering loops for high-quality force operations

**Implementation**: This branch implements safety and quality improvements:

1. **Integer Overflow Protection**: Adds validation in `gimp_temp_buf_new()` to prevent integer overflow when calculating buffer sizes, using `gsize total_size = (gsize) width * height * bpp` with proper bounds checking.

2. **Memory Safety**: Implements NULL pointer checking after `gegl_malloc()` calls and validates that rowstride is sufficient for the required data (`rowstride >= width * bpp`).

3. **Improved Buffer Creation**: Refactors `gimp_temp_buf_new_from_pixbuf()` with additional validation to ensure GdkPixbuf data integrity before buffer creation.

4. **High-Quality Force Activation**: Enables previously disabled high-quality force parameters in the brush core loops, originally developed by Ell but deactivated due to performance concerns. Now optimized for better balance between quality and performance.

5. **Memory Management**: Memory tracking with atomic operations for better thread safety in memory size calculations.

This represents an improvement to paintbrush stability and quality, addressing potential crashes from buffer overflows while enabling better rendering quality.

</div>

<div class="feature-section" id="feature-presets-restore">

## feature-presets-restore

**Purpose**: Tool preset workflow with double-click restoration functionality for immediate preset re-application.

**Role**: Streamlines preset management by allowing users to restore active preset settings without requiring preset switching.

**Files Modified** (1 file, 3 insertions):
- `app/widgets/gimpcontainericonview.c` (3 lines added): Double-click restoration functionality in icon view

**Implementation**: Adds a workflow enhancement to the container icon view system:

1. **Double-Click Restoration**: When a user double-clicks on an already active preset in the icon view, the code now calls `gimp_context_tool_preset_changed()` to restore the tool options to the preset's saved state.

2. **Workflow Efficiency**: This eliminates the previous requirement to select a different preset and then return to the desired preset to restore its settings, reducing workflow friction.

3. **Context Integration**: The implementation leverages the existing context system (`renderer->context`) to trigger the preset restoration, maintaining consistency with the existing architecture.

The change is minimal but addresses a user frustration where preset settings could drift from their saved values during a session, requiring cumbersome preset switching to restore the original configuration.

</div>

<div class="feature-section" id="feature-toolbox">

## feature-toolbox

**Purpose**: Toolbox customization with optional flowbox removal and flexible FG/BG widget positioning and scaling for improved workspace efficiency.

**Role**: Provides users with toolbox layout options to create either a compact interface or maintain the traditional multi-area layout, with control over foreground/background color widget placement and size.

**Files Modified** (2 files, 205 insertions, 104 deletions):
- `app/widgets/gimptoolbox.c` (291 lines modified): Dual toolbox creation modes and flexible FG/BG widget positioning
- `app/widgets/gimptoolpalette.c` (18 lines modified): Enhanced tool palette integration with scaling support

**Implementation**: Implements a flexible toolbox system with two distinct modes:

1. **Dual Toolbox Modes**: Creates two different toolbox layouts based on `config->toolbox_alt_fg_bg`:
   - **Traditional Mode** (`toolbox_create_flowbox()`): Maintains the existing flowbox layout with color, foo, and image areas
   - **Compact Mode** (`toolbox_create_flexible_fg_bg()`): Removes the flowbox and provides only the FG/BG color widget for minimal interface

2. **FG/BG Widget Positioning**: Allows positioning the foreground/background color widget relative to the tool palette:
   - Configurable positions: Top, Bottom, Left, or Right placement
   - Integration with existing configuration system for persistent settings

3. **Scalable Color Widget**: Implements dynamic scaling of the FG/BG color widget:
   - Uses `config->toolbox_scale_fg_bg` for custom scaling factors
   - Automatically adapts to tool icon sizes: `gtk_icon_size_lookup()` determines base size
   - Applies custom scale multiplier for HDPI display support

4. **Conditional Area Management**: Adds null-checking for area widgets to support both modes:
   - Only updates image/foo area renderers when flowbox mode is active
   - Prevents crashes when areas don't exist in compact mode

5. **Configuration Integration**: Binds toolbox behavior to preference settings for real-time layout switching and persistent user preferences.

This provides users with the choice between a traditional multi-area toolbox or a streamlined interface with just the FG/BG color widget, plus control over widget positioning and scaling for different display configurations.

</div>

<div class="feature-section" id="feature-painttool">

## feature-painttool

**Purpose**: Paint tool enhancement providing improved cursor visibility, erase mode indication, simplified brush boundaries, and proper mask erasing behavior.

**Role**: Overhaul of the paint tool user experience with four key improvements focused on cursor feedback, visual clarity, and intuitive erasing behavior.

**Files Modified** (1 file, 315 insertions, 50 deletions):
- `app/tools/gimppainttool.c` (365 lines modified): Complete enhancement of paint tool cursor system and erasing behavior

**Implementation**: This branch delivers four user experience improvements:

1. **Easy Cursor Location**: Ensures paint cursors are always visible and locatable:
   - Implements `gimp_draw_brush_cursor()` with minimum cursor size enforcement
   - Adds `FINDER_SIZE` and `CORE_SIZE` constants for consistent small cursor visibility
   - Creates a small filled contact circle that's always drawn, even when brush outline is disabled
   - Uses `should_locate()` detection (28px threshold) to trigger fallback locator circle for tiny brushes
   - Prevents lost cursors during fine detail work

2. **Erase Mode Indication**: Provides clear visual feedback when in erase mode:
   - Introduces `gimp_is_erasing_paint()` detection for both Eraser Tool and Erase Paint blend mode
   - Automatically switches cursor to dashed circle pattern when erasing is active
   - Uses `gimp_draw_arc_circle()` with customizable dash counts (6 for standard, 12 for selection)
   - Combines dashed outline with central contact circle for precise erase positioning
   - Makes erase mode visually clear

3. **Simple Brush Boundary**: Reduces visual distraction from complex brush shapes:
   - Adds "Simple Brush Boundary" option in Paintbrush Options
   - Replaces complex image brush outlines with clean circular boundaries
   - Implements `draw_brush_circle()` for optimized circular rendering
   - Maintains brush functionality while providing cleaner visual feedback
   - Useful for large, noisy, or complex image brushes

4. **Proper Mask Erasing**: Fixes eraser behavior on layer masks:
   - Detects when working on layer masks using channel operations
   - Automatically uses black color for erasing on masks (instead of background color)
   - Integrates mask detection with existing eraser tool functionality
   - Makes mask editing more intuitive by following standard mask conventions

**Technical Details**:
- Updated include system for MyPaint brush, dynamics, and channel operations
- Drawing algorithms with anti-aliasing support
- Timer-based optimization (`PICK_TIMER_MIN`: 5ms) for performance
- Mathematical precision constants (`EPSILON`: 1e-6) for calculations

These changes improve digital painting workflow by addressing issues with cursor visibility, mode confusion, and mask editing, while maintaining accuracy.

</div>

<div class="feature-section" id="feature-resource-control">

## feature-resource-control

**Purpose**: Resource management system providing improved control over saving, loading, and managing brushes, patterns, gradients, and tool presets.

**Role**: Improves Artbox's resource handling, offering user-controlled saving, batch operations, and more flexible resource management workflows.

**Files Modified** (74 files, 5,179 insertions, 743 deletions):
- **Actions & Commands** (25 files): Updates to brush, dynamics, gradient, palette, pattern, and tool preset actions with new save-as functionality and additional commands
- **Core System** (5 files): `gimpdatafactory.c` (297 insertions), `gimpdata.c/h` (13 modifications), data handling improvements
- **Dialogs** (4 files): New `asset-save-as-dialog.c/h` (556 lines), updated preferences dialog with resource management options
- **Widgets** (15 files): Updates to tool preset editor (1,862 insertions), data editors, and resource factory views
- **Menus** (9 files): Menu systems with simplified options and additional resource-specific actions
- **Scripts** (3 files): New paste-as-brush and copy-as-brush Script-Fu functionality

**Implementation**: Implements 12 features:

1. **Deactivate Automatic Saving**: User preference to control when resource changes are saved
2. **Immediate Saving**: Manual save options to help prevent data loss
3. **Save As Functionality**: Custom naming and versioning for all resource types
4. **Save All Changes**: Batch save operations for all active tool assets
5. **Simpler Menus**: Interface hides rarely used menu items
6. **Brush Editor Enhancements**: Improved brush type handling and creation workflows
7. **Locked Resource Notification**: Visual feedback for read-only resources
8. **Copy/Paste New Brush**: Create new brushes directly from drawable content
9. **Tool Preset Name Display**: Active preset shown in window titles and interface
10. **Preferences Folder Options**: Improved resource folder path management
11. **Resource Filtering**: Optional filtering and tagging system for resource organization
12. **Icon View Preview**: Theme backgrounds for better resource previews

These changes address workflow issues with GIMP's resource management system.

</div>

<div class="feature-section" id="feature-dynamic-output">

## feature-dynamic-output

**Purpose**: Overhaul of brush dynamics processing with angular dynamics, pressure/fade multiplier modes, and angle interpolation.

**Role**: Changes how brush dynamics calculate values, particularly for angular brush behavior and dynamic interactions.

**Files Modified**:
- `app/core/gimpdynamicsoutput.c` (388 lines modified - 271 insertions, 117 deletions)

**Implementation**: Rewrites the dynamics output calculation system with several improvements:

1. **Separate Linear and Angular Processing**: Refactors dynamics calculation to handle linear values (like size, opacity) differently from angular values (brush rotation), providing more appropriate mathematical operations for each.

2. **Pressure/Fade Multiplier Modes**: Adds modes where pressure and fade can act as multipliers rather than additive factors, allowing pressure to scale other dynamics.

3. **Angular Interpolation**: Implements angle interpolation using shortest-path calculation, ensuring brush rotation transitions smoothly.

4. **Fade Initial Angle**: Adds capability for strokes to start at an initial brush angle and transition to dynamically calculated angles over the course of the stroke.

5. **Random Jitter**: Provides controlled random angle jitter (up to ±180°) with user-editable curves.

6. **Error Handling**: Adds validation and error reporting for edge cases like infinite or out-of-range values in fade calculations.

7. **Mathematical Precision**: Ensures all angle calculations handle normalization, wrapping, and edge cases that could cause visual artifacts.

These changes make brush dynamics more predictable and mathematically consistent.

</div>

<div class="feature-section" id="feature-selection">

## feature-selection

**Purpose**: Selection tools with auto-commit, auto-deselect, and fill-on-commit functionality for improved selection workflows.

**Role**: Adds selection capabilities providing automated workflow features for efficient selection operations.

**Files Modified** (3 files, 183 insertions, 4 deletions):
- `app/tools/gimpfreeselecttool.c` (117 insertions, 4 deletions)
- `app/tools/gimpselectionoptions.c` (66 insertions)
- `app/tools/gimpselectionoptions.h` (4 insertions)

**Implementation**: Extends the free selection tool with three workflow enhancements:

1. **Auto-Commit**: Automatically commits selections when the polygon is closed
2. **Fill on Commit**: Optionally fills the selected area when the selection is committed
3. **Auto-Deselect**: Automatically removes the selection after the fill operation

The implementation adds new options to the selection tool options dialog and modifies the free select tool's behavior to handle these workflows while preserving tool control state.

</div>

<div class="feature-section" id="feature-transform-tool">

## feature-transform-tool

**Purpose**: Transformation tools with selection-aware behavior and improved transform control options.

**Role**: Adds object transformation capabilities with flexible selection handling.

**Files Modified** (3 files, 79 insertions, 9 deletions):
- `app/tools/gimptransformoptions.c` (21 insertions, 1 deletion)
- `app/tools/gimptransformoptions.h` (1 insertion)
- `app/tools/gimptransformtool.c` (66 insertions, 5 deletions)

**Implementation**: Adds a "Use Selection" option to transform tools that allows users to control whether transformations apply to the selected area or the entire layer. This provides more flexible transformation behavior:

1. **Selection-Aware Transforms**: New boolean option in transform tool options to toggle between transforming selected areas vs. entire layers
2. **Control Interface**: Integrates the selection option into the transform options GUI with property handling
3. **Transform Logic**: Modifies the core transform tool behavior to respect the selection setting and handle edge cases

This gives users explicit control over transform scope.

</div>

<div class="feature-section" id="feature-filter-restores-last-tool">

## feature-filter-restores-last-tool

**Purpose**: Workflow enhancement that automatically restores the previously active tool after filter operations complete.

**Role**: Maintains tool selection continuity during filter workflows.

**Files Modified** (1 file, 5 insertions, 1 deletion):
- `app/tools/gimpfiltertool.c` (6 lines modified): Enhanced filter tool response handling with context-aware tool restoration

**Implementation**: Implements tool restoration functionality to improve workflow continuity:

1. **Context Integration**: Adds context handling to filter tool operations:
   - Retrieves user context via `gimp_get_user_context(gimp)` for tool state management
   - Integrates with the context system's previous tool tracking (`context->prev_tool_info`)

2. **Dual Response Handling**: Implements tool restoration for both completion scenarios:
   - **OK Response**: After successful filter application (`GTK_RESPONSE_OK`), restores previous tool
   - **Cancel/Escape Response**: After filter cancellation, restores previous tool

3. **Variable Management**: Extracts `gimp` and `context` variables for code structure
   - Maintains existing tool control functionality while adding restoration behavior

4. **Workflow Continuity**: Users return to their previous tool after filter use, reducing manual tool switching.

The implementation uses the context system's previous tool tracking (from `convert-context-all-merged`) to provide tool restoration.

</div>

<div class="feature-section" id="feature-script-fu-plugins">

## feature-script-fu-plugins

**Purpose**: Collection of custom Script-Fu plugins that extend Artbox with workflow automation, layer management, and productivity enhancements.

**Role**: Provides productivity tools and workflow automation specific to Artbox users' needs, extending the application's scripting capabilities through Scheme-based scripting.

**Plugin Categories**: Four distinct categories of functionality:

### Paint Tool Utilities
- **Toggle Paint Mode**: Switch between paint and erase modes using the eraser slider value
- **Toggle Paintbrush Eraser**: Quick toggle between paintbrush and eraser tools
- **Toggle Eraser**: Alternative eraser toggle functionality
- **Add Path Guide**: Creates a locked path guide for drawing straight lines and curves

### Layer Management
- **Group Selected Layers**: Creates a new layer group from selected layers
- **Layer Group To New Image**: Exports layer groups as new image files
- **New Layer From Selection**: Creates a new layer from the current selection
- **Rename Layers**: Batch rename multiple layers with pattern options

### File Management
- **Incremental Save**: Saves numbered versions to a subfolder without overwriting the original
- **Almost Autosave**: Automated saving functionality for workflow protection

### Effects & Utilities
- **Gaussian Glow**: Multi-layered glow effect with successive blurs and opacity control
- **Alpha To Show Mask**: Converts alpha channel information to visible mask display

**Implementation**: These plugins are exclusive to Artbox and use additional commands not available in GIMP. They install as part of Artbox to the data resource folders when built locally or can be found bundled in the AppImage download.

**User Control**: Users can deactivate these plugins through Edit → Preferences → Folders → Plug-ins by removing the `share/artbox/` path.

See the [Plugins documentation](/hub/plugins/folder/) for detailed usage information for each plugin.

</div>

<div class="feature-section" id="feature-dynamic-brush-spacing">

## feature-dynamic-brush-spacing

**Purpose**: Dynamic brush spacing calculation for more predictable and controllable brush behavior.

**Role**: Provides brush dynamics with spacing control for natural stroke appearance.

**Files Modified** (1 file, 2 insertions, 11 deletions):
- `app/paint/gimpbrushcore.c` (13 lines modified)

**Implementation**: Replaces the previous dynamic spacing algorithm with a simpler, more predictable approach:

**Previous Behavior**: Dynamic spacing used a formula where the core spacing was treated as the minimum value, with dynamics adding up to 200% spacing through interpolation.

**New Behavior**: Dynamic spacing now uses direct multiplication (`core->spacing * dyn_spacing`) with a minimum epsilon limit, providing:

1. **Predictable Scaling**: Dynamics directly multiply the base spacing value
2. **Intuitive Control**: Users can more easily predict how dynamics will affect brush spacing
3. **Simplified Logic**: Removes complex calculation code in favor of direct multiplication
4. **Consistent Behavior**: Spacing behavior is now consistent with other brush dynamics

This change makes brush spacing dynamics more intuitive and easier to control.

</div>

<div class="feature-section" id="feature-motion-buffer">

## feature-motion-buffer

**Purpose**: Motion buffer system with stabilization support for smooth stroke rendering and improved input responsiveness.

**Role**: Stroke smoothing and motion prediction with stabilization distance control.

**Files Modified** (5 files, 179 insertions, 33 deletions):
- `app/display/gimpdisplayshell-tool-events.c` (48 insertions, 1 deletion)
- `app/display/gimpmotionbuffer.c` (145 insertions, 5 deletions)
- `app/display/gimpmotionbuffer.h` (11 insertions, 1 deletion)
- `app/paint/gimppaintcore.c` (4 insertions, 1 deletion)
- `app/tools/gimppainttool-paint.c` (4 insertions, 1 deletion)

**Implementation**: Updates the motion buffer system with stabilization features:

1. **Stabilization Distance Integration**: Connects paint tool stabilization distance settings to the motion buffer
2. **Stroke Initiation**: Improves stroke beginning with better coordinate tracking and stabilization-aware initialization
3. **Stabilization State Management**: Tracks when stabilization periods end and adjusts paint core coordinates
4. **Motion Event Enhancement**: Extends motion event handling to support stabilization distance parameters and state tracking
5. **Paint Tool Integration**: Guards against non-paint tools while providing handling for paint tools with stabilization support

The system provides more responsive input handling while maintaining smooth stroke quality through buffering and stabilization.

</div>

<div class="feature-section" id="feature-smooth-stroke">

## feature-smooth-stroke

**Purpose**: Stroke smoothing system with velocity-responsive algorithms and mathematical stroke analysis.

**Role**: Improves stroke quality and smoothness with smoothing algorithms and testing capabilities.

**Files Modified** (1 file, 593 insertions, 48 deletions):
- `app/paint/gimppaintcore.c` (641 lines modified)

**Implementation**: Implements a stroke smoothing system with mathematical analysis and testing capabilities:

1. **Velocity-Responsive Smoothing**: Uses velocity exponent (3.0) to control how responsive smoothing is to velocity changes
2. **Multiple Stroke Types**: Supports different stroke patterns including linear, slow-to-fast, fast-to-slow, and slow-in-slow-out for testing
3. **Averaging System**: Implements coordinate, pressure, and angle averaging with weighted calculations
4. **Testing Infrastructure**: Includes testing framework with data tables and validation output for stroke smoothing function validation
5. **Mathematical Precision**: Uses epsilon values and floating-point calculations for consistent smoothing behavior
6. **GUI Integration**: Scales GUI slider values (0-100) to mathematical range (0-1) for calculation

Key smoothing features:
- **Position Smoothing**: Averages stroke coordinates with velocity weighting
- **Pressure Smoothing**: Smooths pressure variations for consistent brush response
- **Direction Smoothing**: Maintains smooth directional changes in brush strokes
- **Testing Output**: Optional console output with stroke data tables for algorithm validation

These changes improve stroke quality and provide validation capabilities.

</div>

<div class="feature-section" id="feature-eraser">

## feature-eraser

**Purpose**: Enhanced eraser functionality with layer mask awareness and improved color picker behavior.

**Role**: Improved erasing tools with context-aware erasing and better workflow integration.

**Files Modified** (2 files, 9 insertions, 2 deletions):
- `app/paint/gimperaser.c` (6 insertions)
- `app/tools/gimperasertool.c` (5 insertions, 2 deletions)

**Implementation**: Provides two key improvements to the eraser tool's behavior:

1. **Layer Mask Awareness**: When erasing on layer masks, the eraser automatically uses black as the paint color instead of the background color, ensuring proper mask editing behavior regardless of the current background color setting.

2. **Foreground Color Picker**: Changes the eraser's color picker from background to foreground color picking, with updated status text to reflect this change. This provides more intuitive color picking behavior for users.

The changes include:
- Automatic black color selection for layer mask erasing operations
- Foreground color picker integration with appropriate status messages
- Improved context awareness for different drawable types
- Comment noting future enhancement potential for user-configurable color picker target

These changes make the eraser tool more context-aware while maintaining its core functionality.

</div>

<div class="feature-section" id="feature-snapping">

## feature-snapping

**Purpose**: Snapping functionality with separate path snapping distance control and vector tool behavior.

**Role**: Alignment and positioning tools with context-aware snapping behavior.

**Files Modified** (3 files, 20 insertions, 4 deletions):
- `app/core/gimpimage-snap.c` (6 insertions, 2 deletions)
- `app/core/gimpimage-snap.h` (2 insertions)
- `app/display/gimpdisplayshell.c` (16 insertions, 2 deletions)

**Implementation**: Enhances the snapping system with two improvements:

1. **Separate Path Snapping Distance**: Introduces independent epsilon values for path snapping (`epsilon_path_x` and `epsilon_path_y`) allowing different snapping distances for paths versus other snap targets.

2. **Vector Tool Snap Suppression**: Disables path snapping when the Vector Tool is active, preventing unwanted snapping behavior during path editing operations.

Key features:
- **Independent Path Snap Distance**: Uses `snap_path_distance` configuration for path-specific snapping tolerance
- **Context-Aware Behavior**: Automatically disables path snapping during vector tool operations
- **Enhanced API**: Extends the snap point API to support separate epsilon values for different snap types
- **User Control**: Provides more granular control over snapping behavior for different object types

These changes improve alignment workflows while maintaining behavior that adapts to the current tool context.

</div>

<div class="feature-section" id="feature-path-editing">

## feature-path-editing

**Purpose**: Path editing with automatic visibility control and improved stroke connection functionality for vector workflows.

**Role**: Vector path manipulation with better user experience and workflow automation.

**Files Modified** (4 files, 47 insertions, 5 deletions):
- `app/display/gimptoolpath.c` (28 insertions, 4 deletions)
- `app/tools/gimpvectoroptions.c` (19 insertions, 1 deletion)
- `app/tools/gimpvectoroptions.h` (1 insertion)
- `app/tools/gimpvectortool.c` (4 insertions)

**Implementation**: Enhances path editing with automatic visibility management and improved functionality:

1. **Automatic Path Visibility**:
   - Adds "Visible when created" property to path tools
   - Automatically makes newly created paths visible in the layers panel
   - Eliminates the workflow issue of "invisible" paths that users can't find

2. **Property Management**:
   - New `PROP_VISIBLE` property in both tool path and vector options
   - Property handling with getters/setters for the visibility feature
   - Default visibility set to TRUE for immediate user feedback

3. **Stroke Connection Logic**:
   - Enhanced anchor selection and stroke extension functionality
   - Better handling of anchor-to-anchor connections for polygon creation
   - Improved readability in anchor selection logic

4. **User Experience Improvements**:
   - New paths are immediately visible without manual intervention
   - More intuitive path creation workflow
   - Reduces confusion for users working with vector paths

These changes address a usability issue where users create paths that aren't immediately visible.

</div>

<div class="feature-section" id="feature-colour-picker">

## feature-colour-picker

**Purpose**: Color picker with Alt key sample-merged toggle and improved user interface for sampling mode switching.

**Role**: Color selection and sampling with keyboard-driven workflow optimization.

**Files Modified** (2 files, 6 insertions, 6 deletions):
- `app/actions/layers-actions.c` (4 insertions, 2 deletions)
- `menus/layers-menu.ui` (8 insertions, 4 deletions)

**Implementation**:

1. **Alt Key Toggle**: Implements Alt key modifier to toggle sample-merged state during color picking operations:
   - Press Alt to toggle between layer-only and merged sampling
   - Both key press and release toggle the state for immediate feedback
   - Allows rapid switching between sampling modes without accessing tool options

2. **UI Labels**: Updates the sample-merged option label to "Sample merged (Alt)" to indicate the keyboard shortcut

3. **Workflow**: Enables dynamic sampling mode changes during active color picking operations, eliminating the need to stop the current operation or access tool options

Key benefits:
- **Keyboard-Driven Efficiency**: Quick mode switching with Alt key
- **Real-Time Control**: Change sampling behavior during active operations
- **UI Indication**: Label shows available keyboard shortcut
- **Seamless Workflow**: No interruption of color picking tasks

These changes improve the color picker workflow by providing access to both layer-specific and merged color sampling modes through keyboard shortcuts.

</div>

<div class="feature-section" id="feature-layer-pop-up-menu">

## feature-layer-pop-up-menu

**Purpose**: Layer context menu with simplified labels and reduced complexity for improved workflow efficiency and cleaner interface.

**Role**: Layer management interface with optimized menu organization.

**Files Modified** (2 files, 6 insertions, 6 deletions):
- `app/actions/layers-actions.c` (4 insertions, 2 deletions)
- `menus/layers-menu.ui` (8 insertions, 4 deletions)

**Implementation**: Simplifies the layer popup menu for better usability and reduced clutter:

1. **Simplified Action Labels**: Updates layer action labels for brevity and clarity:
   - "Duplicate Layers" → "Duplicate Selected"
   - "Delete Layers" → "Delete Selected"
   - Maintains keyboard shortcuts (`Ctrl+Shift+D` for duplicate)

2. **Menu Streamlining**: Comments out submenu sections that are rarely used:
   - **Blend Space submenu**: Removes advanced blend space options
   - **Composite Space submenu**: Hides composite space controls
   - **Composite Mode submenu**: Removes composite mode options
   - **Color Tag submenu**: Hides color tagging functionality
   - **Transform section**: Removes resize, resize-to-image, and scale options

3. **Focused Functionality**: Keeps essential layer operations while removing advanced features that clutter the context menu:
   - Maintains core layer operations (new, duplicate, delete, masks)
   - Preserves text layer functionality
   - Keeps essential layer management features

Key benefits:
- **Cleaner Interface**: Reduced menu complexity
- **Improved Workflow**: Faster access to commonly used functions
- **Reduced Cognitive Load**: Fewer menu options to navigate
- **Consistent Labeling**: More logical and concise action names
- **Focused Functionality**: Emphasis on core layer operations

These changes streamline the layer context menu to prioritize commonly used operations.

</div>

<div class="feature-section" id="feature-supress-warning-messages">

## feature-supress-warning-messages

**Purpose**: Warning message suppression for cleaner application output and improved user experience in production environments.

**Role**: Improved user experience through reduced message noise while maintaining essential error reporting.

**Files Modified** (3 files, 7 insertions, 32 deletions):
- `app/text/gimpfontfactory.c` (4 insertions, 2 deletions)
- `app/widgets/gimperrorconsole.c` (27 deletions)
- `plug-ins/script-fu/libscriptfu/scheme-marshal-return.c` (8 insertions, 4 deletions)

**Implementation**: Reduces verbose warning output across multiple subsystems:

1. **Font Loading Warnings**: Comments out font loading warnings in `gimpfontfactory.c` that inform about unsupported fonts being ignored.

2. **Error Console Simplification**: Streamlines the error console interface:
   - Removes decorative icons and complex formatting from error messages
   - Eliminates excessive spacing and visual elements
   - Simplifies message display to essential text content only
   - Maintains error message content while reducing visual clutter

3. **Script-Fu Debug Suppression**: Comments out several Script-Fu debugging messages:
   - Suppresses warnings about NULL GIMP objects returned by PDB procedures
   - Removes debug output for object ID returns
   - Eliminates warnings about invalid GFile returns from PDB calls

Key improvements:
- **Cleaner Console Output**: Reduced warning noise during normal operation
- **Simplified Error Display**: Error console shows essential information
- **Production-Ready Output**: More appropriate warning levels for end-user environments
- **Maintained Functionality**: All core error reporting remains intact

</div>

<div class="feature-section" id="feature-simple-sliders">

## feature-simple-sliders

**Purpose**: Simplified slider interface with enhanced text selection and improved visual positioning for better usability.

**Role**: Enhanced control interface with streamlined slider design and better user interaction.

**Files Modified** (4 files, 29 insertions, 21 deletions):
- `libgimpwidgets/gimpspinbutton.c` (18 insertions, 1 deletion)
- `libgimpwidgets/gimpspinbutton.h` (1 insertion)
- `libgimpwidgets/gimpspinscale.c` (30 insertions, 20 deletions)
- `libgimpwidgets/gimpwidgets.def` (1 insertion)

**Implementation**: Simplifies slider interfaces while adding useful functionality:

1. **Text Selection Enhancement**: Adds `gimp_spin_button_select_all()` function that automatically selects all text in spin button entries, making it easier for users to replace values entirely

2. **Improved Text Positioning**: Shifts slider text 4 pixels to the right for better visual alignment and readability

3. **Simplified Target Detection**: Streamlines the complex target detection logic in spin scales, removing intricate layout-based position calculations (20 lines removed) in favor of simpler event-based targeting

4. **Double-Click Selection**: Changes double-click behavior to directly target number selection, making text editing more intuitive

5. **Code Simplification**: Removes complex pixel-perfect layout calculations while maintaining essential functionality, resulting in cleaner and more maintainable code

Key improvements:
- **Better User Interaction**: Easier text selection and editing in spin buttons
- **Visual Enhancement**: Improved text positioning for better readability
- **Simplified Logic**: Reduced complexity in target detection while maintaining functionality
- **Enhanced Accessibility**: More predictable click and selection behavior

This feature makes sliders more user-friendly by providing better text handling and simplified interaction patterns.

</div>

<div class="feature-section" id="feature-warp-update">

## feature-warp-update

**Purpose**: Major warp tool overhaul with layer group support, mask handling, and extensive functionality enhancements for professional warping workflows.

**Role**: Enhanced transformation capabilities with comprehensive warp functionality and group layer support.

**Files Modified** (5 files, 1,562 insertions, 278 deletions):
- `app/tools/gimpwarptool.c` (1,726 insertions, 278 deletions - major rewrite)
- `app/tools/gimpwarpoptions.c` (74 insertions, deletions)
- `app/tools/gimpwarpoptions.h` (5 insertions)
- `app/tools/gimpwarptool.h` (5 insertions)
- `app/widgets/gimpdrawabletreeview-filters.c` (30 insertions, deletions)

**Implementation**: Represents a comprehensive rewrite and expansion of the warp tool with 1,562 lines of new functionality:

1. **Layer Group Support**:
   - **Group Mask Warping**: Optional warping of layer group masks with "Warp group masks" option
   - **Opaque Group Masks**: Automatic filling of layer group masks with white after warping
   - **Group Margin Control**: Configurable layer group expansion margin (16-2048 pixels, default 256)

2. **Enhanced Size Controls**:
   - **Improved Size Range**: Minimum effect size increased from 1.0 to 12.0 pixels for better control
   - **Better Scale Limits**: Updated scale limits to prevent overly small brush sizes that cause issues

3. **Advanced Warping Options**:
   - Three new boolean and integer properties for group handling
   - Enhanced tool options GUI with additional controls
   - Comprehensive property management for all new features

4. **Major Core Rewrite**: The 1,726-line change to `gimpwarptool.c` represents a fundamental enhancement of the warp tool's core functionality, adding sophisticated group layer support and advanced warping algorithms

Key features:
- **Professional Group Workflows**: Full support for warping complex layer group hierarchies
- **Mask Management**: Intelligent handling of layer group masks during warp operations
- **Enhanced Control**: Better size limits and margin controls for precise warping
- **Comprehensive Options**: New GUI elements for all advanced features

This update transforms the warp tool from a basic transformation tool into a professional-grade warping system capable of handling complex layer structures.

</div>

<div class="feature-section" id="feature-gui-size-tweaks">

## feature-gui-size-tweaks

**Purpose**: Enhanced curve view interaction with larger control points and improved click targets for better usability on high-DPI displays.

**Role**: Interface optimization for better display adaptation and improved precision control.

**Files Modified** (1 file, 4 modifications)

**Implementation**: Improves curve editor usability through strategic size adjustments:

1. **Larger Click Targets**: Increases `POINT_MAX_DISTANCE` from 16.0 to 24.0 pixels, expanding the clickable area around curve control points by 50%. This makes it significantly easier to select and manipulate curve points, especially on high-resolution displays.

2. **Enhanced Visual Feedback**: Increases `CIRCLE_RADIUS` from 3 to 9 pixels (300% increase), making curve control points much more visible and easier to target. The larger radius provides:
   - Better visibility of control points on modern high-DPI screens
   - Improved accessibility for users with visual difficulties
   - More precise visual feedback during curve editing

Key benefits:
- **Better High-DPI Support**: Appropriately sized controls for modern display resolutions
- **Improved Accessibility**: Larger targets are easier to interact with for all users
- **Enhanced Precision**: Clearer visual indication of control point positions
- **Modern UI Standards**: Brings curve controls in line with contemporary interface expectations

This small but impactful change significantly improves the curve editing experience, making it more comfortable and precise for users working with dynamics, color curves, and other curve-based controls in Artbox.

</div>

<div class="feature-section" id="feature-paintbrush-slider-tool-tips">

## feature-paintbrush-slider-tool-tips

**Purpose**: Enhanced tooltip control for paintbrush sliders with user preference integration for cleaner interface when tooltips are disabled.

**Role**: Improved user interface with configurable tooltip system respecting global preferences.

**Files Modified** (1 file, 5 insertions):
- `app/tools/gimppaintoptions-gui.c` (5 insertions)

**Implementation**: Adds tooltip management to paint tool sliders based on user preferences:

1. **Preference-Aware Tooltips**: Integrates with the global `gui_config->show_tool_tips` setting to control tooltip display on paint option sliders

2. **Clean Interface Option**: When users disable tooltips in preferences, the paint tool sliders now respect this setting and remove their tooltips, providing a cleaner, less cluttered interface

3. **Consistent Behavior**: Ensures that paint tool option sliders behave consistently with the rest of the application's tooltip system

4. **Non-Intrusive Enhancement**: Only affects tooltip display when tooltips are globally disabled - normal tooltip functionality remains unchanged when tooltips are enabled

Key benefits:
- **User Preference Respect**: Paint sliders now honor global tooltip preferences
- **Cleaner Interface**: Users who prefer minimal interfaces can disable all tooltips including paint sliders
- **Consistent Experience**: Uniform tooltip behavior across the entire application
- **Configurable UI**: Users have control over interface verbosity level

This small but important enhancement ensures that users who prefer streamlined interfaces without tooltips can have a truly clean experience throughout Artbox, including in the paint tool options where tooltips were previously forced on regardless of global preferences.

</div>

<div class="feature-section" id="feature-additional-script-fu">

## feature-additional-script-fu

**Purpose**: Major Script-Fu API expansion with eraser toggle functionality, enhanced context management, and comprehensive PDB extensions for advanced scripting automation.

**Role**: Extended scripting capabilities and automation features with significant API additions.

**Files Modified** (19 files, 1,576 insertions, 54 deletions):
- **Core Context System** (2 files): `gimpcontext.c` (106 insertions), `gimpcontext.h` (3 insertions)
- **Layer System** (2 files): `gimplayer.c` (371 insertions), `gimplayer.h` (5 insertions)
- **PDB Commands** (4 files): `context-cmds.c` (309 insertions), `item-cmds.c` (64 insertions), `layer-cmds.c` (80 insertions), `internal-procs.c` (2 modifications)
- **LibGIMP Interface** (5 files): Major expansions to context, item, and layer PDB interfaces (334 total insertions)
- **PDB Groups** (4 files): Enhanced `context.pdb` (179 insertions), `item.pdb`, `layer.pdb`, and `stddefs.pdb`

**Implementation**: Provides extensive Script-Fu functionality through four major enhancement categories:

1. **Eraser Toggle System**: Implements sophisticated tool switching with previous tool memory:
   - `gimp_context_eraser_toggle()`: Smart toggle between eraser and previous tool
   - `gimp_context_eraser_paintbrush_toggle()`: Direct eraser/paintbrush switching
   - `gimp_context_get_eraser_active()`: Query eraser tool state
   - Previous tool tracking with proper memory management

2. **Enhanced Context Management**: Extends context functionality with tool change detection and state management for seamless tool switching workflows

3. **Expanded Layer PDB Functions**: Adds 371 lines of new layer manipulation functions providing comprehensive layer control through Script-Fu

4. **Comprehensive PDB Extensions**: Major additions to context, item, and layer PDB groups with 800+ lines of new API functions for advanced scripting capabilities

Key scripting enhancements:
- **Tool State Management**: Advanced tool switching with memory and state detection
- **Context Extensions**: Enhanced context manipulation for complex scripting workflows
- **Layer Automation**: Comprehensive layer manipulation functions for batch operations
- **API Completeness**: Fills gaps in the PDB API for professional scripting needs

This represents the largest single expansion of Artbox's scripting API, providing essential functionality for automation scripts and advanced user workflows.

</div>

<div class="feature-section" id="feature-selection-highlight">

## feature-selection-highlight

**Purpose**: Enhanced selection visualization with automatic highlighting and improved visual feedback for selection operations.

**Role**: Enhanced selection visualization and user feedback with intelligent highlighting system.

**Files Modified** (10 files, 65 insertions, 135 deletions):
- **Selection Commands** (1 file): `select-commands.c` (18 insertions, 1 deletion)
- **Display System** (3 files): `gimpdisplay.c` (16 insertions, 2 deletions), `gimpdisplayshell.c` (35 insertions, 3 deletions), `gimptoolrectangle.c` (47 deletions)
- **Tool Options** (6 files): Streamlined rectangle tool options removing 130 lines of code across crop and select tools

**Implementation**: Provides automatic selection highlighting with intelligent visual feedback:

1. **Automatic Highlight on Select All**: When "Select All" is executed, automatically creates a highlight rectangle around the entire selection with padding (±20 pixels) and 50% opacity for clear visual feedback

2. **Dynamic Highlight Updates**: Integrates selection highlighting into the display flush system, ensuring highlights update automatically when selections change or images are opened

3. **Streamlined Tool Options**: Removes redundant rectangle tool option code (130+ lines deleted) while maintaining essential functionality, simplifying the codebase

4. **Enhanced Display Integration**: Connects selection highlighting to the core display system for consistent behavior across all selection operations

Key features:
- **Visual Selection Feedback**: Clear highlighting when selections are made or modified
- **Automatic Highlight Management**: Highlights appear and update without user intervention
- **Code Simplification**: Removes redundant rectangle tool option implementations
- **Consistent Behavior**: Selection highlights work uniformly across all selection tools and commands

This enhancement improves the user experience by providing clear visual feedback for selection operations while simplifying the underlying code structure.

</div>

<div class="feature-section" id="feature-gfig">

## feature-gfig

**Purpose**: Enhanced GFig plugin with significantly larger preview size for better geometric shape visualization and precision editing.

**Role**: Enhanced geometric tool functionality with improved visual feedback.

**Files Modified** (1 file, 1 insertion, 1 deletion):
- `plug-ins/gfig/gfig-preview.h` (1 modification)

**Implementation**: Dramatically improves the GFig plugin's usability through a simple but impactful change:

1. **Enlarged Preview Size**: Increases the `PREVIEW_SIZE` constant from 400 to 1024 pixels (156% increase), providing:
   - **Better Detail Visibility**: Users can see fine details in geometric shapes more clearly
   - **Improved Precision**: Easier to position and adjust shape parameters with visual feedback
   - **Modern Display Support**: Better utilization of contemporary screen resolutions
   - **Enhanced Workflow**: Less need to zoom in/out or squint at small preview areas

Key benefits:
- **Enhanced Usability**: Larger preview makes the GFig plugin much more pleasant to use
- **Better Visual Feedback**: Users can more accurately assess their geometric constructions
- **Modern UI Standards**: Preview size appropriate for current display technologies
- **Improved Accessibility**: Larger preview is easier to see for users with visual difficulties

This simple but effective enhancement transforms the GFig plugin experience from a cramped, difficult-to-use interface to a spacious, modern geometric construction tool suitable for detailed work.

</div>

<div class="feature-section" id="feature-status-bar">

## feature-status-bar

**Purpose**: Enhanced status bar with intelligent workflow reminders and visibility controls for improved user guidance and interface management.

**Role**: Enhanced status information and user feedback with context-aware notifications.

**Files Modified** (2 files, 128 insertions, 4 deletions):
- `app/display/gimpstatusbar.c` (130 insertions, 4 deletions)
- `app/display/gimpstatusbar.h` (2 insertions)

**Implementation**: Significantly enhances the status bar with intelligent notification system and interface improvements:

1. **Smart Widget Visibility**: Changes default visibility behavior for cursor label and unit combo to only show when relevant, reducing interface clutter when these elements aren't needed.

2. **Autosave Reminder System**:
   - Adds persistent "• activate autosave" reminder label with 70% transparent red text
   - Helps users remember to enable the autosave functionality for data protection
   - Uses CSS styling for visual consistency and subtle appearance

3. **Selection Visibility Indicator**:
   - Adds "• Selection is hidden, View > Show Selection" notification
   - Alerts users when selections are present but not visible due to display settings
   - Prevents confusion about "lost" selections
   - Uses distinctive red coloring with 70% transparency for visual prominence

4. **Enhanced CSS Integration**:
   - Implements proper CSS providers for custom styling
   - Provides consistent visual appearance for notification elements
   - Uses subtle transparency effects for non-intrusive notifications

5. **Intelligent Workflow Guidance**:
   - Context-aware reminders that appear when relevant
   - Helps prevent common workflow issues (lost work, invisible selections)
   - Educates users about important features through persistent but subtle notifications

Key benefits:
- **Workflow Protection**: Reminds users about important data-saving features
- **Reduced Confusion**: Clear indicators for interface state issues
- **Cleaner Interface**: Smart hiding of unnecessary elements
- **User Education**: Subtle guidance about important application features
- **Professional Polish**: Sophisticated notification system with proper styling

This enhancement transforms the status bar from a simple information display into an intelligent workflow assistant that guides users and prevents common issues.

</div>

<div class="feature-section" id="feature-fullscreen-is-fullscreen">

## feature-fullscreen-is-fullscreen

**Purpose**: True fullscreen mode implementation that automatically hides docks for genuine distraction-free creative work environment.

**Role**: Enhanced display mode for focused creative work with complete interface simplification.

**Files Modified** (1 file, 4 insertions):
- `app/actions/view-commands.c` (4 insertions)

**Implementation**: Enhances fullscreen mode to provide genuine full-screen experience:

1. **Automatic Dock Hiding**: When entering fullscreen mode, automatically sets `hide-docks` to true, ensuring that:
   - All toolboxes and docks are hidden
   - The entire screen is dedicated to the canvas
   - No interface elements remain visible to distract from the artwork

2. **True Fullscreen Experience**: Unlike the default GIMP fullscreen that may leave some interface elements visible, this implementation provides:
   - Complete canvas focus with zero distractions
   - Maximum screen real estate for artwork
   - Genuine immersive creative environment

3. **Synchronized State Management**: The dock hiding state is properly synchronized with the fullscreen state, ensuring consistent behavior when entering and exiting fullscreen mode.

Key benefits:
- **Genuine Fullscreen**: True distraction-free environment for creative work
- **Automatic Behavior**: No manual dock hiding required when entering fullscreen
- **Maximum Canvas Space**: Complete screen utilization for artwork viewing and editing
- **Focused Workflow**: Eliminates visual distractions during intensive creative sessions

This enhancement is particularly valuable for artists who need to focus entirely on their work without any interface distractions, providing a true "canvas-only" mode for maximum creative concentration.

</div>

<div class="feature-section" id="feature-style-settings">

## feature-style-settings

**Purpose**: Comprehensive visual style customization system with configurable line widths, alpha transparency, and color scheme adjustments for improved interface personalization.

**Role**: Interface customization and visual theme control with advanced styling options.

**Files Modified** (2 files, 73 insertions, 10 deletions):
- `app/display/gimpcanvas-style.c` (81 insertions, 4 deletions)
- `app/display/gimpdisplayshell-selection.c` (2 insertions, 1 deletion)

**Implementation**: Provides extensive customization of visual display elements with user-configurable parameters:

1. **Configurable Line Widths**: Replaces hardcoded line widths with user-configurable settings:
   - **Selection Lines**: Configurable `selection_line_width` (default was 1.0)
   - **Path Lines**: Configurable `path_line_width` (default was 3.0)
   - **Layer Outline Lines**: Dynamic line width based on user preferences

2. **Alpha Transparency Control**: Adds comprehensive alpha transparency management:
   - **Selection Alpha**: Configurable `selection_line_alpha` for selection visibility
   - **Layer Alpha**: Applied to all layer outline colors (foreground, background, group, mask)
   - **Graduated Transparency**: Outside selection lines use 33% of the base alpha for subtle appearance

3. **Enhanced Color Scheme**:
   - Changes selection outline background from gray to black for better contrast
   - Applies alpha values dynamically to all visual elements
   - Maintains color consistency across all canvas display elements

4. **Comprehensive Style Application**: Alpha and width settings applied to:
   - Selection in/out styles
   - Layer boundary styles
   - Layer group boundaries
   - Layer mask boundaries
   - Vector path displays

Key benefits:
- **User Customization**: Complete control over visual appearance through preferences
- **High-DPI Support**: Configurable line widths adapt to different display densities
- **Accessibility**: Adjustable alpha values for users with different visual needs
- **Professional Appearance**: Sophisticated transparency effects for modern UI aesthetics
- **Consistent Styling**: Unified customization system across all canvas elements

This enhancement transforms Artbox's visual appearance from fixed styling to a fully customizable interface that users can adapt to their specific needs, display characteristics, and aesthetic preferences.

</div>

<div class="feature-section" id="feature-max-brush-size">

## feature-max-brush-size

**Purpose**: Architecture-aware maximum brush and pattern size limits with enhanced support for high-resolution artwork on 64-bit systems.

**Role**: Extended brush size range for diverse artistic needs with platform-optimized limits.

**Files Modified** (2 files, 10 insertions, 4 deletions):
- `app/core/gimpbrushclipboard.c` (7 insertions, 2 deletions)
- `app/core/gimppatternclipboard.c` (7 insertions, 2 deletions)

**Implementation**: Implements intelligent size limits based on system architecture:

1. **64-bit Architecture Optimization**:
   - Increases maximum brush size from 1024 to 8192 pixels on 64-bit systems (8x increase)
   - Increases maximum pattern size from 1024 to 8192 pixels on 64-bit systems
   - Leverages the increased memory capabilities of modern 64-bit architectures

2. **Platform-Aware Limits**: Uses conditional compilation to set appropriate limits:
   - **64-bit systems**: 8192 pixel maximum for both brushes and patterns
   - **32-bit systems**: Maintains conservative 1024 pixel limit for memory safety
   - **Architecture Detection**: Uses `ARCH_X86_64` macro for automatic platform detection

3. **Enhanced Creative Capabilities**: The 8x size increase enables:
   - High-resolution digital art workflows
   - Large-scale texture work and pattern creation
   - Professional print-resolution artwork
   - Detailed brush work for poster and banner design

4. **Memory Safety**: Maintains conservative limits on older 32-bit systems to prevent memory-related issues while maximizing capabilities on modern hardware.

Key benefits:
- **Modern Hardware Utilization**: Takes full advantage of 64-bit architecture capabilities
- **Professional Workflow Support**: Enables high-resolution creative work
- **Platform Optimization**: Appropriate limits for each architecture type
- **Backward Compatibility**: Maintains safe limits on older systems

This enhancement is particularly valuable for professional digital artists working on high-resolution projects, print media, and large-scale digital artwork where brush and pattern sizes beyond the traditional 1024-pixel limit are essential.

</div>

<div class="feature-section" id="feature-duplicate-layer-and-clear">

## feature-duplicate-layer-and-clear

**Purpose**: Layer duplication with automatic content clearing for efficient template creation and layer organization workflows.

**Role**: Enhanced layer management operations providing streamlined duplicate-and-clear functionality.

**Files Modified** (5 files, 56 insertions, 1 deletion):
- `app/actions/layers-actions.c` (7 insertions)
- `app/actions/layers-commands.c` (43 insertions)
- `app/actions/layers-commands.h` (3 insertions)
- `app/widgets/gimphelp-ids.h` (1 insertion)
- `menus/layers-menu.ui` (3 insertions, 1 deletion)

**Implementation**: Adds a new layer operation that combines duplication with content clearing in a single action:

1. **Duplicate and Clear Command**: New `layers_duplicate_and_clear_cmd_callback()` function that:
   - Creates exact duplicates of selected layers with full metadata preservation
   - Automatically clears the content of the duplicated layers using `gimp_drawable_edit_clear()`
   - Maintains proper layer hierarchy and positioning relative to original layers
   - Handles multiple selected layers in batch operations

2. **Menu Integration**: Adds "D_uplicate and Clear" option to the layers menu with:
   - Appropriate icon (GIMP_ICON_OBJECT_DUPLICATE)
   - Descriptive tooltip explaining the functionality
   - Proper help system integration

3. **Undo Group Management**: Wraps the entire operation in a single undo group (`GIMP_UNDO_GROUP_LAYER_ADD`) so users can undo the entire duplicate-and-clear operation as one action

4. **Layer Selection Management**: Automatically selects the newly created cleared layers after the operation, providing immediate feedback and ready-to-use layers

This feature is particularly useful for:
- Creating layer templates with preserved properties but empty content
- Setting up layer structures for repetitive workflows
- Batch creation of cleared layers with specific configurations
- Maintaining layer organization while providing clean starting points

</div>

<div class="feature-section" id="feature-data-factory-filter">

## feature-data-factory-filter

**Purpose**: User-controlled resource filtering system with configurable tag entry visibility for streamlined resource management workflows.

**Role**: Enhanced resource organization and filtering capabilities with optional interface elements.

**Files Modified** (1 file, 8 insertions, 2 deletions):
- `app/widgets/gimpdatafactoryview.c` (10 insertions, 2 deletions)

**Implementation**: Provides user control over resource filtering interface elements based on preferences:

1. **Configurable Tag Entry Visibility**: Links tag entry widgets to the `config->resource_filtering` preference setting:
   - **Query Tag Entry**: Only shows when resource filtering is enabled in preferences
   - **Assign Tag Entry**: Only displays when resource filtering is active
   - **User Choice**: Users can hide filtering elements if they prefer simpler interfaces

2. **Smart Widget Management**: Replaces hardcoded `gtk_widget_show()` calls with conditional `gtk_widget_set_visible()` based on configuration:
   - Prevents null pointer issues with proper widget existence checks
   - Maintains widget functionality when visible
   - Completely hides filtering elements when disabled

3. **Cleaner Interface Option**: When resource filtering is disabled, the interface becomes:
   - Less cluttered without tag entry fields
   - Simplified for users who don't use tagging systems
   - Focused on basic resource browsing and selection

4. **Enhanced Configuration Integration**: Properly integrates with the GUI configuration system to respect user preferences for interface complexity.

Key benefits:
- **User Preference Respect**: Interface adapts to user's filtering preference settings
- **Simplified Interface**: Users can hide complex filtering features they don't use
- **Reduced Clutter**: Optional removal of tag-related interface elements
- **Configurable Complexity**: Users control interface sophistication level
- **Consistent Behavior**: Resource filtering visibility applies across all resource types

This enhancement allows users to customize their resource management interface complexity, hiding advanced filtering features when they prefer simpler, more focused resource browsing experiences.

</div>

<div class="feature-section" id="feature-jitter">

## feature-jitter

**Purpose**: Enhanced brush jitter with mathematically correct uniform distribution option for natural variation and improved randomization quality.

**Role**: Enhanced brush dynamics providing superior random stroke variation with proper statistical distribution.

**Files Modified** (1 file, 15 insertions, 2 deletions):
- `app/paint/gimpbrushcore.c` (17 insertions, 2 deletions)

**Implementation**: Improves brush jitter randomization with statistically accurate distribution options:

1. **Uniform Disk Distribution**: Adds option for proper uniform distribution over a circular area:
   - **Mathematical Accuracy**: Uses `sqrt(u)` for radius sampling to achieve true uniform distribution
   - **Natural Appearance**: Eliminates center-bias that occurs with linear radius sampling
   - **Professional Quality**: Provides mathematically correct randomization for natural-looking strokes

2. **Configurable Distribution**: Controlled by `paint_options->brush_uniform_jitter` setting:
   - **Uniform Mode**: `jitter_dist = dyn_jitter * sqrt(rand_u)` for even distribution
   - **Legacy Mode**: `jitter_dist = dyn_jitter * rand_u` for backward compatibility
   - **User Choice**: Artists can select preferred jitter behavior

3. **Enhanced Random Sampling**: Improves the random number generation approach:
   - Uses dedicated `rand_u` variable for cleaner random value handling
   - Maintains the same angle randomization for directional consistency
   - Preserves existing jitter magnitude controls

Key benefits:
- **Mathematically Correct**: True uniform distribution over circular jitter area
- **Natural Appearance**: Eliminates artificial center clustering in brush strokes
- **Professional Quality**: Provides statistical accuracy expected in professional art tools
- **Backward Compatibility**: Maintains option for original behavior
- **Enhanced Realism**: More natural-looking random variation in brush strokes

This enhancement addresses a fundamental issue in brush randomization where linear radius sampling creates unnatural clustering toward the center of the jitter area, replacing it with proper uniform distribution that produces more natural and visually pleasing random brush variations.

</div>

<div class="feature-section" id="feature-recent-layer-mode-group">

## feature-recent-layer-mode-group

**Purpose**: Sophisticated recent layer modes tracking system with persistent storage and intelligent combo box grouping for streamlined layer blending workflows.

**Role**: Major user experience enhancement that provides quick access to frequently used layer modes through persistent memory and optimized interface grouping.

**Files Modified** (7 files, 598 insertions, 48 deletions):
- `app/gui/gui.c` (8 insertions): Application lifecycle integration for recent modes persistence
- `app/operations/layer-modes/gimp-layer-modes.c` (481 insertions, 48 deletions): Core recent modes tracking system
- `app/operations/layer-modes/gimp-layer-modes.h` (15 insertions): API declarations for recent modes functionality
- `app/operations/operations-enums.c` (2 insertions): Enumeration support for recent modes
- `app/operations/operations-enums.h` (1 insertion): Header enumeration definitions
- `app/widgets/gimplayermodebox.c` (5 insertions, 1 deletion): Layer mode box integration
- `app/widgets/gimplayermodecombobox.c` (134 insertions, 1 deletion): Enhanced combo box with recent modes grouping

**Implementation**: This branch implements a comprehensive recent layer modes system that dramatically improves blending workflow efficiency:

1. **Persistent Recent Modes Tracking**:
   - Implements `gimp_layer_modes_init_recent()` and `gimp_layer_modes_exit_recent()` for session persistence
   - Automatically saves recent modes to dedicated file regardless of session settings
   - Loads previously used modes on application startup for immediate availability

2. **Application Lifecycle Integration**:
   - Integrates recent modes initialization during `gui_restore_after_callback()`
   - Ensures recent modes are saved during `gui_exit_callback()` for session continuity
   - Provides reliable persistence across application restarts

3. **Enhanced Combo Box Functionality**:
   - Major upgrade to `gimplayermodecombobox.c` (134 new lines) with recent modes grouping
   - Intelligent organization placing frequently used modes at the top for quick access
   - Maintains existing categorization while adding recent usage patterns

4. **Core Infrastructure**:
   - Extensive enhancement to `gimp-layer-modes.c` (481 lines) implementing the tracking algorithms
   - New API functions for recent mode management and persistence
   - Integration with existing layer mode enumeration system

5. **User Experience Benefits**:
   - Eliminates need to scroll through long lists of layer modes to find commonly used ones
   - Provides contextual access to modes based on actual usage patterns
   - Maintains user workflow continuity across sessions

This represents a significant improvement to layer blending workflows, transforming a cumbersome mode selection process into an intelligent, adaptive system that learns from user behavior.
