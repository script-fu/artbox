---
type: docs
url: "hub/technical-reference/folder/Convert-Branches"
---

# Convert Branches

Convert branches modify GIMP master to support Artbox features and provide foundational changes for the entire system.

## Branch Overview

{{< cards >}}
  {{< card link="#convert-to-artbox" title="convert-to-artbox" subtitle="Main integration branch - merges all convert branches" >}}
  {{< card link="#convert-app-core-item" title="convert-app-core-item" subtitle="Item geometry and hierarchy utility functions" >}}
  {{< card link="#convert-app-core-image" title="convert-app-core-image" subtitle="Single-selection convenience functions" >}}
  {{< card link="#convert-app-core-grouplayer" title="convert-app-core-grouplayer" subtitle="Hierarchical child retrieval with recursive traversal" >}}
  {{< card link="#convert-app-core-gimppickable-auto-shrink" title="convert-app-core-gimppickable-auto-shrink" subtitle="Auto-shrink pickable objects" >}}
  {{< card link="#convert-app-config" title="convert-app-config" subtitle="Application configuration system" >}}
  {{< card link="#convert-meson" title="convert-meson" subtitle="Build system modifications" >}}
  {{< card link="#convert-dynamics-editor" title="convert-dynamics-editor" subtitle="Dynamics editor interface improvements" >}}
  {{< card link="#convert-context-all-merged" title="convert-context-all-merged" subtitle="Context system enhancements" >}}
  {{< card link="#convert-paintbrush-all-merged" title="convert-paintbrush-all-merged" subtitle="Comprehensive paintbrush system overhaul" >}}
  {{< card link="#convert-force-artbox-config" title="convert-force-artbox-config" subtitle="Artbox configuration enforcement" >}}
  {{< card link="#convert-name" title="convert-name" subtitle="Application name changes from GIMP to Artbox" >}}
  {{< card link="#convert-brush-aspect-ratio" title="convert-brush-aspect-ratio" subtitle="Brush aspect ratio enhancements" >}}
  {{< card link="#convert-boolean-options" title="convert-boolean-options" subtitle="Boolean option handling improvements" >}}
  {{< card link="#convert-tool-tips-option" title="convert-tool-tips-option" subtitle="Tool tips configuration system" >}}
  {{< card link="#convert-help-id" title="convert-help-id" subtitle="Help system identification" >}}
  {{< card link="#convert-curve-view" title="convert-curve-view" subtitle="Curve editing interface enhancements with 4K display support" >}}
  {{< card link="#convert-icons" title="convert-icons" subtitle="Icon replacements and updates" >}}
  {{< card link="#convert-dialogs" title="convert-dialogs" subtitle="Dialog system modifications" >}}
  {{< card link="#convert-issue-templates" title="convert-issue-templates" subtitle="Issue template modifications" >}}
  {{< card link="#convert-mnemonics" title="convert-mnemonics" subtitle="Keyboard mnemonic handling" >}}
  {{< card link="#convert-tool-events" title="convert-tool-events" subtitle="Tool event handling system" >}}
  {{< card link="#convert-localization-messaging" title="convert-localization-messaging" subtitle="Suppresses plugin localization error messages" >}}
  {{< card link="#convert-broken-pipe" title="convert-broken-pipe" subtitle="Suppresses plugin communication error warnings" >}}
  {{< card link="#convert-display-options" title="convert-display-options" subtitle="Display configuration options" >}}
  {{< card link="#convert-supress-timer-prints" title="convert-supress-timer-prints" subtitle="Timer print suppression" >}}
  {{< card link="#convert-brush-preview" title="convert-brush-preview" subtitle="Brush preview functionality" >}}
  {{< card link="#convert-commands-dockable" title="convert-commands-dockable" subtitle="Visual grid interface for custom commands and plugins with dual-language execution support" >}}
  {{< card link="#convert-gitlab-ci" title="convert-gitlab-ci" subtitle="Complete CI/CD pipeline with AppImage infrastructure (2,993 lines)" >}}
{{< /cards >}}

---

<div class="feature-section" id="convert-to-artbox">

## convert-to-artbox

**Purpose**: Main integration branch that merges all convert branches.

**Role**: Common base layer for all feature development.

**Files Modified**: All files from merged convert branches

**Implementation**: Serves as the integration point where all convert branches are merged together to create the common base that feature branches build upon.

</div>

<div class="feature-section" id="convert-app-core-item">

## convert-app-core-item

**Purpose**: Adds utility functions for item geometry calculation, hierarchy analysis, and layer type detection.

**Role**: Foundation layer providing core item management utilities needed by other branches for item operations.

**Files Modified**:
- `app/core/gimpitem.c` (62 lines added - 4 new utility functions)
- `app/core/gimpitem.h` (7 lines added - function declarations)

**Implementation**: Introduces four utility functions to the core item system:

1. **`gimp_item_get_bounding_box()`**: Calculates the bounding rectangle of any item by combining its offset position with its dimensions, used for layout and positioning operations.

2. **`gimp_item_get_depth()`**: Determines how deeply nested an item is in the layer hierarchy, with protection against circular references (max 1000 iterations). Returns -1 if circular reference detected.

3. **`gimp_item_is_group_layer()`**: Type-safe detection of group layers, providing identification of layer groups vs. regular layers.

4. **`gimp_item_is_basic_layer()`**: Identifies basic (non-group) layers by checking if an item is a layer but not a group layer.

These utilities form the foundation for layer management, selection operations, and hierarchy-based features throughout Artbox. The bounding box calculation is particularly important for automation scripts and selection tools.

</div>

<div class="feature-section" id="convert-app-core-image">

## convert-app-core-image

**Purpose**: Adds convenience functions for single-selection operations, simplifying workflows when working with individual items.

**Role**: Streamlines single-item selection workflows by providing dedicated functions for common single-selection scenarios.

**Files Modified**:
- `app/core/gimpimage.c` (35 lines added - 2 new convenience functions)
- `app/core/gimpimage.h` (5 lines added - function declarations)

**Implementation**: Introduces two convenience functions that simplify single-selection workflows:

1. **`gimp_image_get_single_selected_drawable()`**: Returns a single drawable if exactly one is selected, or NULL otherwise. This eliminates the need to manually check selection counts and extract single items from lists, making single-item operations much cleaner and more readable.

2. **`gimp_image_set_single_selected_layer()`**: Convenience wrapper for selecting a single layer by creating a temporary list, calling the multi-selection function, and cleaning up. This provides a simpler API for selecting just one layer.

These functions improve code readability and reduce boilerplate when dealing with single-selection scenarios, which are common in user workflows. They form building blocks for script automation and simplified tool interactions.

</div>

<div class="feature-section" id="convert-app-core-grouplayer">

## convert-app-core-grouplayer

**Purpose**: Group layer functionality improvements.

**Purpose**: Adds hierarchical child retrieval function for group layers with optional recursive nesting support.

**Role**: Enables efficient traversal and manipulation of complex layer hierarchies in group layer structures.

**Files Modified**:
- `app/core/gimpgrouplayer.c` (36 lines added - new traversal function)
- `app/core/gimpgrouplayer.h` (2 lines added - function declaration)

**Implementation**: Introduces a utility function:

**`gimp_group_layer_get_all_child_items()`**: Retrieves all child items from a group layer with configurable recursion control. When `get_nested` is TRUE, it recursively traverses nested group layers to collect all descendants in a flattened list. When FALSE, it returns only direct children.

The function uses safe iteration over the group's children container and includes recursive traversal for nested groups. This is useful for operations that need to work on entire layer hierarchies, such as:
- Batch operations on all layers in a group structure
- Layer selection and filtering within complex hierarchies
- Export operations that need to process all nested content
- Script automation that works with group layer contents

This function enables bulk operations on complex layer trees.

</div>

<div class="feature-section" id="convert-app-core-gimppickable-auto-shrink">

## convert-app-core-gimppickable-auto-shrink

**Purpose**: Auto-shrink functionality with background color detection and expanded shrinking algorithms for optimized memory usage and improved cropping operations.

**Role**: Memory management and performance optimization that provides background detection for auto-shrinking operations.

**Files Modified** (4 files, 280 insertions, 142 deletions):
- `app/actions/image-commands.c` (2 insertions): Added handling for new AUTO_SHRINK_BLACK and AUTO_SHRINK_UNIFORM cases
- `app/actions/layers-commands.c` (2 insertions): Added handling for new shrink modes in layer cropping operations
- `app/core/gimppickable-auto-shrink.c` (274 insertions, 142 deletions): Major enhancement with intelligent background detection algorithms
- `app/core/gimppickable-auto-shrink.h` (2 insertions): New function declarations for background color detection

**Implementation**: This branch enhances the auto-shrink system with background detection and expanded shrinking capabilities:

1. **Enhanced Shrinking Modes**: Expands the internal `AutoShrinkType` enumeration to include:
   - `AUTO_SHRINK_BLACK = 3`: Specialized mode for detecting and shrinking black backgrounds
   - Support for `GIMP_AUTO_SHRINK_UNIFORM`: Uniform color background detection mode

2. **Background Detection**: Introduces the new `gimp_pickable_guess_bgcolor()` function that analyzes pickable objects to determine background colors within specified regions (`x1, x2, y1, y2`). This enables auto-shrinking decisions based on content analysis.

3. **Enhanced Command Integration**: Updates both image and layer command handling to properly process the new shrinking modes:
   - `image-commands.c`: Extends crop-to-content operations with black and uniform background handling
   - `layers-commands.c`: Ensures layer cropping operations respect the new shrinking modes

4. **Improved Algorithm Architecture**: Refactors the core auto-shrink implementation (274 lines of changes) to support color analysis and background detection algorithms, enabling more accurate automatic cropping operations.

This enhancement provides users with auto-cropping capabilities that can detect and handle various background color scenarios, improving workflow efficiency for content with uniform or black backgrounds.

</div>

<div class="feature-section" id="convert-app-config">

## convert-app-config

**Purpose**: Plugin path configuration system that adds data directory plugin search paths for improved plugin discovery and deployment flexibility.

**Role**: Infrastructure enhancement that expands plugin loading capabilities to support both user and system plugin directories.

**Files Modified** (1 file, 2 insertions):
- `libgimpconfig/gimpconfig-path.c` (2 lines added): Enhanced plugin path building with data directory support

**Implementation**: This branch enhances the plugin path configuration system with a strategic addition to plugin discovery:

1. **Expanded Plugin Search Paths**: Modifies `gimp_config_build_plug_in_path()` to include the data directory in the plugin search path:
   - **Original path**: `${gimp_dir}` → `${gimp_plug_in_dir}`
   - **Enhanced path**: `${gimp_dir}` → `${gimp_data_dir}` → `${gimp_plug_in_dir}`

2. **Improved Plugin Discovery**: The addition of `${gimp_data_dir}` provides:
   - **System-wide plugin support**: Plugins can be installed in shared data directories
   - **Package manager compatibility**: Better integration with Linux distribution packaging
   - **Deployment flexibility**: Multiple installation locations for different plugin types

3. **Search Path Priority**: Maintains logical search order:
   - User directory (`${gimp_dir}`) - highest priority for user-specific plugins
   - Data directory (`${gimp_data_dir}`) - system/shared plugins
   - Plugin directory (`${gimp_plug_in_dir}`) - standard plugin installation location

4. **Backward Compatibility**: The change is additive, preserving existing plugin loading behavior while expanding capabilities.

This enhancement enables more flexible plugin deployment strategies and better integration with system package managers, particularly important for Artbox's distribution and plugin ecosystem.

</div>

<div class="feature-section" id="convert-meson">

## convert-meson

**Purpose**: Build system rebranding from GIMP to Artbox through data directory path modification in the Meson build configuration.

**Role**: Infrastructure change that establishes Artbox's distinct data directory structure and installation paths.

**Files Modified** (1 file, 1 insertion, 1 deletion):
- `meson.build` (1 line modified): Data directory path configuration change from project-based to Artbox-specific

**Implementation**: This branch implements a build system change that establishes Artbox's independent identity:

1. **Data Directory Rebranding**: Changes the `gimpdatadir` configuration from:
   - **Original**: `get_option('datadir') / project_subdir` (uses dynamic project name)
   - **Updated**: `get_option('datadir') / 'artbox'` (uses hardcoded 'artbox' identifier)

2. **Installation Path Impact**: This change affects all data file installations:
   - **System themes**: Now installed to `/usr/share/artbox/` instead of `/usr/share/gimp/`
   - **Resources**: Brushes, patterns, gradients use Artbox-specific paths
   - **Documentation**: Help files and documentation use Artbox directories
   - **Plugins**: Data-dependent plugins reference Artbox data locations

3. **Independence from Project Variables**: By hardcoding 'artbox', this ensures:
   - **Brand consistency**: All installations clearly identify as Artbox
   - **Separation from GIMP**: Prevents conflicts with existing GIMP installations
   - **Predictable paths**: Data locations are consistent regardless of build configuration

4. **Build System Integration**: Works with the existing Meson infrastructure while:
   - Maintaining compatibility with existing build options
   - Preserving other directory variables (`gimpplugindir`, `gimpsysconfdir`)
   - Ensuring proper data directory references throughout the build

This simple change is important for Artbox's independent distribution and ensures users can install Artbox alongside GIMP without data directory conflicts.

</div>

<div class="feature-section" id="convert-dynamics-editor">

## convert-dynamics-editor

**Purpose**: Dynamics editor interface overhaul with input label management, improved function signatures, and modernized GTK widget handling.

**Role**: Architectural improvement to the dynamics editor providing better maintainability, user interface consistency, and improved input mapping visualization.

**Files Modified** (2 files, 279 insertions, 40 deletions):
- `app/widgets/gimpdynamicseditor.c` (100 insertions, 5 deletions): Enhanced dynamics editor with input label management and modernized widget handling
- `app/widgets/gimpdynamicsoutputeditor.c` (219 insertions, 2 deletions): Major expansion of output editor functionality with enhanced UI components

**Implementation**: This branch represents an architectural improvement to the dynamics editor system:

1. **Enhanced Function Signatures**: Modernizes function parameters throughout the dynamics editor system:
   - `gimp_dynamics_editor_add_output_row()`: Enhanced with `GtkWidget **input_labels` parameter for improved label management
   - `gimp_dynamics_editor_init_output_editors()`: Added input labels parameter for better component tracking
   - `dynamics_check_button_new()`: Enhanced with row label and input label parameters for improved checkbox management

2. **Input Label Management System**: Introduces input label tracking with `GtkWidget *input_labels[7]` array, enabling better coordination between different dynamics input channels and their visual representation.

3. **Modernized GTK Widget Handling**: Updates deprecated GTK functions for better compatibility:
   - Replaces `gtk_widget_show()` with `gtk_widget_set_visible(widget, TRUE)` for improved clarity and future GTK compatibility
   - Enhanced widget visibility management throughout the interface

4. **UI Architecture**: Expansion of the output editor (219 lines added) with improved:
   - Mapping matrix layout with better visual organization
   - Scrollability for complex dynamics configurations
   - Tooltip systems for user guidance
   - Reset confirmation dialogs to prevent accidental data loss

5. **Component Integration**: Better integration between the main dynamics editor and individual output editors, providing more cohesive user experience and improved state management.

This modernization provides a foundation for dynamics editing while maintaining backward compatibility and improving user experience.

</div>

<div class="feature-section" id="convert-context-all-merged">

## convert-context-all-merged

**Purpose**: Context system enhancement providing previous tool tracking and eraser toggle functionality for improved tool workflow and context-aware operations.

**Role**: Core infrastructure improvement that enables tool switching behaviors and context-aware features throughout Artbox.

**Files Modified** (2 files, 7 insertions, 1 deletion):
- `app/core/gimpcontext.c` (4 insertions): Previous tool tracking implementation and memory management
- `app/core/gimpcontext.h` (4 insertions, 1 deletion): New context fields and function declarations

**Implementation**: This branch introduces tool context enhancements that form the foundation for tool behaviors:

1. **Previous Tool Tracking**: Adds `prev_tool_info` field to the `GimpContext` structure, enabling the system to remember the previously active tool. This is useful for tool restoration workflows and toggle behaviors.

2. **Tool Management**: Implements tool transition handling in `gimp_context_real_set_tool()`:
   - Stores current tool as previous tool before switching: `g_set_object (&context->prev_tool_info, context->tool_info)`
   - Maintains tool history for workflow restoration features

3. **Memory Management**: Lifecycle management for the new context fields:
   - Initialization: Sets `prev_tool_info` to NULL during context initialization
   - Cleanup: Implements `g_clear_object (&context->prev_tool_info)` in dispose method to prevent memory leaks

4. **Eraser Toggle Foundation**: Declares `gimp_context_eraser_toggle()` function in the header, providing the foundation for eraser toggle functionality that allows switching between tools and eraser mode.

5. **API Extension**: Extends the context API to support tool management patterns needed by Artbox's tool workflows, particularly for paint tools and selection tools.

This enhancement enables tool switching behaviors, including the ability to restore previous tools after filter operations, implement tool toggles, and provide context-aware tool behavior throughout the application.

</div>

<div class="feature-section" id="convert-paintbrush-all-merged">

## convert-paintbrush-all-merged

**Purpose**: Paintbrush system transformation with brush engine, tool options overhaul, and brush control interface for digital art creation.

**Role**: Core foundation providing the paintbrush architecture that enables digital art workflows and brush behavior throughout Artbox.

**Files Modified** (12 files, 1386 insertions, 493 deletions):
- `app/config/gimpguiconfig.c` (34 insertions): Brush reset and update button configuration options
- `app/config/gimpguiconfig.h` (2 insertions): GUI configuration property declarations for brush controls
- `app/dialogs/preferences-dialog.c` (14 insertions): Preference dialog integration for brush settings
- `app/paint/gimpbrushcore.c` (3 insertions, 1 deletion): Enhanced brush core functionality
- `app/paint/gimppaintcore.c` (8 insertions, 1 deletion): Improved paint core operations
- `app/paint/gimppaintoptions.c` (445 insertions, 3 deletions): Major paint options enhancement with advanced features
- `app/paint/gimppaintoptions.h` (46 insertions, 1 deletion): Extensive paint options structure expansion
- `app/tools/gimppaintoptions-gui.c` (1287 insertions, 111 deletions): Complete GUI overhaul for paint tool options
- `app/tools/gimppainttool.h` (5 insertions): Paint tool header enhancements
- `app/widgets/gimpcontainerpopup.c` (12 insertions, 1 deletion): Container popup improvements
- `app/widgets/gimpviewablebox.c` (11 insertions, 1 deletion): Viewable box widget enhancements
- `libgimpwidgets/gimppropwidgets.c` (12 insertions): Property widget improvements

**Implementation**: This branch represents the most significant transformation to the paintbrush system, establishing Artbox as a digital art platform:

1. **Brush Control Interface**: Complete redesign of the paint options GUI (1287 lines added) featuring:
   - Brush parameter controls with precision sliders
   - Brush dynamics integration
   - Real-time brush preview and feedback systems
   - Brush behavior customization options

2. **Paint Options Enhancement**: Expansion of paint options system (445 lines added) including:
   - Brush behavior parameters
   - Opacity and flow controls
   - Blending mode options
   - Brush dynamics support

3. **Brush Management**: Introduction of user-configurable brush control features:
   - `PROP_SHOW_BRUSH_RESET_BUTTONS`: Optional reset buttons for quick brush parameter restoration
   - `PROP_SHOW_BRUSH_UPDATE_BUTTONS`: Optional update buttons for brush setting management
   - Brush preset integration

4. **Widget System**: Improvements to widget handling (46 property additions) including:
   - Better container popup behavior for brush selection
   - Improved viewable box functionality for brush previews
   - Property widget responsiveness and usability

5. **Paint Engine**: Core improvements to paint engine architecture:
   - Brush core performance and rendering
   - Improved paint core operations for better responsiveness
   - Better integration with brush features

This transformation establishes the foundation for digital art creation, providing artists with the brush control and responsiveness expected in modern digital art applications.

</div>

<div class="feature-section" id="convert-force-artbox-config">

## convert-force-artbox-config

**Purpose**: Configuration directory enforcement that ensures Artbox uses its own dedicated configuration directory separate from GIMP installations.

**Role**: Infrastructure component that prevents configuration conflicts and ensures Artbox maintains its own user settings and preferences.

**Files Modified** (1 file, 4 insertions):
- `libgimpbase/gimpenv.c` (4 lines added): Configuration directory path enforcement for Artbox

**Implementation**: This branch implements an identity separation at the configuration level:

1. **Dedicated Configuration Directory**: Forces Artbox to use `.config/Artbox/3.0/default` as the configuration directory when the `GIMP3_DIRECTORY` environment variable is not set:
   ```c
   /* Force a different directory for Artbox config files */
   if (! env_gimp_dir)
     env_gimp_dir = ".config/Artbox/3.0/default";
   ```

2. **Environment Variable Respect**: Maintains compatibility with manual configuration directory specification through the `GIMP3_DIRECTORY` environment variable, allowing advanced users to override the default location if needed.

3. **Clean Separation**: Ensures that Artbox installations do not interfere with existing GIMP configurations, allowing both applications to coexist on the same system without conflicts.

4. **Cross-Platform Compatibility**: Uses proper path construction that works across different operating systems while maintaining the Artbox-specific directory structure.

This change establishes Artbox as a completely independent application from GIMP at the configuration level, preventing user confusion and ensuring that settings, brushes, presets, and other user data remain separate between the applications.

</div>

<div class="feature-section" id="convert-name">

## convert-name

**Purpose**: Rebranding from GIMP to Artbox throughout the application interface, about dialogs, and user-facing text.

**Role**: Identity transformation establishing Artbox as a distinct application with its own branding and attribution.

**Files Modified**:
- `app/about.h` (12 modifications - name, acronym, copyright, and license text)
- `app/actions/dialogs-actions.c` (8 modifications - dialog action descriptions)
- `app/dialogs/about-dialog.c` (6 modifications - about dialog title and website)
- `app/display/gimpdisplayshell-callbacks.c` (48 deletions - removes GIMP-specific drop zone graphics and unstable version warnings)
- `app/errors.c` (2 modifications - development version message)

**Implementation**: Renaming operation that transforms core identity elements:

1. **Application Identity**: Changes GIMP acronym and "GNU Image Manipulation Program" to "Artbox" throughout the interface
2. **Copyright Attribution**: Updates copyright to include "Mark Sweeney" alongside original GIMP developers
3. **License Text**: Modifies license statements to reference "Artbox" instead of "GIMP"
4. **About Dialog**: Updates dialog titles, website URL (to https://script-fu.github.io/artbox/), and website labels
5. **Help Text**: Changes all user-facing help text and tooltips to reference Artbox
6. **Visual Cleanup**: Removes GIMP-specific drop zone graphics (Wilber mascot) and development version warnings that don't apply to Artbox
7. **Error Messages**: Updates development version messages for Artbox context

This branch establishes Artbox as a distinct application while maintaining attribution to the original GIMP developers. The changes affect all user-visible text and branding elements.

</div>

<div class="feature-section" id="convert-brush-aspect-ratio">

## convert-brush-aspect-ratio

**Purpose**: Brush aspect ratio enhancements with normalized linear range for predictable distortion.

**Role**: Enhanced brush shape control with simplified aspect ratio interface.

**Files Modified**:
- `app/core/gimpbrush-transform.cc`
- `app/core/gimpbrush.c`
- `app/core/gimpbrushgenerated.c`
- `app/paint/gimpbrushcore.c`
- `app/pdb/context-cmds.c`
- `app/widgets/gimpbrusheditor.c`
- `pdb/groups/context.pdb`

**Implementation**: Replaces the old non-linear aspect ratio range of -20 to 20 with a simplified linear range from -1 to 1. Value of 1 means undistorted, 0 represents high distortion, and -1 flips the brush stamp, providing predictable linear distortion and finer control over brush appearance.

</div>

<div class="feature-section" id="convert-boolean-options">

## convert-boolean-options

**Purpose**: Boolean option default changes that improve workflow efficiency by enabling device tool sharing and immediate filter merging by default.

**Role**: User experience enhancement that establishes more productive default behaviors for workflow scenarios.

**Files Modified** (2 files, 2 insertions, 2 deletions):
- `app/config/gimpguiconfig.c` (1 insertion, 1 deletion): Device tool sharing default changed from FALSE to TRUE
- `app/tools/gimpfilteroptions.c` (1 insertion, 1 deletion): Filter merge default changed from FALSE to TRUE

**Implementation**: This branch implements two default value changes that improve user workflow:

1. **Device Tool Sharing Enhancement**: Changes the default behavior for `devices-share-tool` from `FALSE` to `TRUE`:
   - **Impact**: When multiple input devices (mouse, tablet, stylus) are used, they now share the same tool by default
   - **Benefit**: Eliminates the confusion of having different tools selected on different devices, providing a more intuitive experience for users switching between input methods
   - **Use Case**: Beneficial for digital artists who frequently switch between mouse and tablet/stylus input

2. **Filter Merge Default**: Changes the default behavior for filter operations from `FALSE` to `TRUE`:
   - **Impact**: Filters are now immediately merged/applied by default rather than remaining as editable non-destructive filters
   - **Benefit**: Provides immediate results for users who prefer direct editing workflows
   - **Flexibility**: Users can still disable this option to access non-destructive filter editing when needed

These changes reflect Artbox's focus on streamlined workflows and user-friendly defaults, reducing the need for users to manually configure preferences while maintaining flexibility for users.

</div>

<div class="feature-section" id="convert-tool-tips-option">

## convert-tool-tips-option

**Purpose**: Tooltip system enhancement that provides user-configurable tooltip display based on application preferences for improved user experience control.

**Role**: User interface customization that allows users to control when tooltips are displayed, providing cleaner interfaces for experienced users while maintaining help for beginners.

**Files Modified** (2 files, 17 insertions, 3 deletions):
- `app/widgets/gimpdockbook.c` (13 insertions, 3 deletions): Enhanced dockbook tab widget creation with tooltip configuration integration
- `app/widgets/gimptoolbutton.c` (7 insertions): Tool button enhancements with GUI configuration integration

**Implementation**: This branch introduces tooltip management that respects user preferences:

1. **Configuration-Aware Tooltip Display**: Integrates with the GUI configuration system to conditionally display tooltips:
   ```c
   if (gui_config->show_tool_tips)
     show_tips = gimp_dockable_get_blurb (dockable);
   ```

2. **Dockbook Integration**: Modifies the dockbook tab widget creation process to:
   - Access the context and GUI configuration through `gimp_dock_get_context()` and `GIMP_GUI_CONFIG()`
   - Conditionally set tooltip text based on user preferences
   - Maintain help data functionality while respecting tooltip preferences

3. **Tool Button Configuration**: Adds GUI configuration support to tool buttons through `config/gimpguiconfig.h` integration, enabling tooltip behavior customization for tool buttons as well.

4. **Variable Management**: Better organization of local variables in tab widget creation with clearer naming and initialization patterns.

5. **User Experience Control**: Allows users to disable tooltips for a cleaner interface while preserving help system functionality for when tooltips are enabled.

This enhancement provides users with control over tooltip display, supporting both experienced users who prefer minimal interfaces and new users who benefit from contextual help information.

</div>

<div class="feature-section" id="convert-help-id">

## convert-help-id

**Purpose**: Help system enhancement with additional path editing help identifier for user guidance and documentation access.

**Role**: Help system expansion that provides specific help context for path editing operations, improving user access to relevant documentation.

**Files Modified** (1 file, 1 insertion):
- `app/widgets/gimphelp-ids.h` (1 line added): New help identifier for path end edit operations

**Implementation**: This branch adds a help system enhancement:

1. **Path Editing Help Expansion**: Introduces `GIMP_HELP_PATH_END_EDIT` help identifier specifically for path end edit operations:
   ```c
   #define GIMP_HELP_PATH_END_EDIT "gimp-path-end-edit"
   ```

2. **User Guidance**: Provides a dedicated help identifier that can be referenced throughout the application when users need guidance on ending path edit operations, ensuring consistent access to relevant help documentation.

3. **Help System Completeness**: Fills a gap in the help identifier system where path editing operations had identifiers for import, export, and general edit operations, but lacked specific guidance for ending edit sessions.

4. **Documentation Integration**: Enables the help system to provide context-specific documentation for path editing workflows, particularly important for users learning complex vector path manipulation.

While this is a small change (single line addition), it represents a usability improvement that ensures users have access to appropriate help documentation for all path editing operations, supporting Artbox's focus on user-friendly workflows.

</div>

<div class="feature-section" id="convert-curve-view">

## convert-curve-view

**Purpose**: Enhancements to the Curve View interface used in the Dynamics Editor and Curves Filter for improved usability and 4K display compatibility.

**Role**: UI improvements that enhance the curve editing experience across all curve-based tools and filters.

**Files Modified** (414 insertions, 231 deletions):
- `app/widgets/gimpcurveview.c` (642 lines modified - major interface overhaul)
- `app/widgets/gimpcurveview.h` (3 lines modified - interface updates)

**Implementation**: Based on feature-test analysis, this branch implements four improvements:

1. **Grid Line Visibility**: Added rendering modes to ensure grid lines are consistently visible across different background tones, solving visibility issues that made curve editing difficult in various visual contexts.

2. **Coordinate Display Refinement**: Redesigned the X,Y coordinate display to eliminate obtrusive block highlighting, improving readability and reducing visual distraction for a cleaner interface.

3. **Curve Point Visibility**: Visibility of curve control points specifically for 4K displays where points could become difficult to see, ensuring accessibility across all display resolutions.

4. **Shift-Key Curve Movement**: Implemented functionality to move all curve points together when holding the Shift key, enabling synchronized curve adjustments for efficient editing workflows.

These changes represent a usability improvement for all curve-based operations in Artbox, making the interface more accessible.

</div>

<div class="feature-section" id="convert-icons">

## convert-icons

**Purpose**: Icon system enhancement with new editor-specific icons and document management icon additions for improved visual consistency and user interface clarity.

**Role**: Visual identity and user interface improvement that provides specialized icons for different editor types and enhanced document management workflows.

**Files Modified** (1 file, 6 insertions):
- `libgimpwidgets/gimpicons.h` (6 lines added): New icon definitions for chain states, document operations, and editor-specific icons

**Implementation**: This branch expands the icon system with targeted additions:

1. **Chain State Icons**: Adds `GIMP_ICON_CHAIN_HORIZONTAL_DATA_LOSS` for indicating potential data loss scenarios in chain-linked controls, providing better visual feedback for destructive operations.

2. **Document Management Icons**: Introduces batch document operation icons:
   - `GIMP_ICON_DOCUMENTS_SAVE`: For saving multiple documents simultaneously
   - `GIMP_ICON_DOCUMENTS_SAVE_AS`: For batch save-as operations
   - These support document management workflows in Artbox

3. **Editor-Specific Icons**: Adds dedicated editor icons for improved visual distinction:
   - `GIMP_ICON_EDITOR_BRUSH`: Specialized icon for brush editor interfaces
   - `GIMP_ICON_EDITOR_DYNAMICS`: Specialized icon for dynamics editor interfaces

These additions provide more precise visual communication in the user interface, helping users quickly identify different types of operations and editor contexts while supporting Artbox's workflow capabilities.

</div>

<div class="feature-section" id="convert-dialogs">

## convert-dialogs

**Purpose**: Dialog factory enhancement that updates editor dialog icons to use the new specialized editor-specific icons for improved visual consistency and user interface clarity.

**Role**: User interface improvement that leverages the enhanced icon system to provide better visual distinction between different types of editor dialogs.

**Files Modified** (1 file, 2 insertions, 2 deletions):
- `app/dialogs/dialogs.c` (icon replacements): Dialog factory registration with updated editor-specific icons

**Implementation**: This branch updates the dialog factory system to use the newly available editor-specific icons:

1. **Brush Editor Icon Update**: Changes the brush editor dialog registration from `GIMP_ICON_BRUSH` to `GIMP_ICON_EDITOR_BRUSH`:
   - Provides visual distinction between brush resources and brush editing functionality
   - Improves user interface clarity by using purpose-specific iconography

2. **Dynamics Editor Icon Update**: Changes the dynamics editor dialog registration from `GIMP_ICON_DYNAMICS` to `GIMP_ICON_EDITOR_DYNAMICS`:
   - Distinguishes between dynamics resources and dynamics editing interfaces
   - Maintains visual consistency with other editor-specific icons

3. **User Experience**: The specialized icons help users quickly identify editor dialogs versus resource browsers, reducing confusion and improving workflow efficiency.

This change leverages the icon enhancements from convert-icons to provide a user interface where different types of dialogs are clearly distinguished through appropriate iconography.

</div>

<div class="feature-section" id="convert-issue-templates">

## convert-issue-templates

**Purpose**: Transformation of GitLab issue templates from GIMP-specific reporting formats to streamlined Artbox-focused templates that improve issue reporting efficiency and relevance.

**Role**: Development workflow improvement that provides focused and efficient issue reporting templates tailored to Artbox development needs.

**Files Modified** (2 files, 10 insertions, 55 deletions):
- `.gitlab/issue_templates/Default.md` (50 deletions, additions): Streamlined default issue template focused on Artbox-specific reporting
- `.gitlab/issue_templates/feature.md` (15 deletions, additions): Simplified feature request template

**Implementation**: This branch implements an overhaul of issue reporting templates:

1. **Simplified Issue Reporting Structure**: Replaces the complex GIMP issue template with a streamlined Artbox-focused format:
   - **"What issue bothers you in Artbox?"**: Direct, user-friendly problem identification
   - **"Does it also happen in GIMP?"**: Acknowledges the relationship while focusing on Artbox
   - **"How can I make it happen in Artbox?"**: Clear reproduction request
   - **"Reproduction steps"**: Structured problem replication guide

2. **Removed GIMP-Specific Content**: Eliminates GIMP-specific references, version requirements, and complex environment specifications that don't apply to Artbox development workflow.

3. **User Experience**: The simplified templates reduce barrier to entry for issue reporting, making it easier for users to provide useful feedback without overwhelming technical requirements.

4. **Focused Development Workflow**: Templates are designed to gather essential information for Artbox development while acknowledging the relationship to upstream GIMP without being constrained by GIMP's more complex reporting requirements.

This transformation supports Artbox's goal of being more accessible and user-friendly, extending this philosophy to the development and issue reporting process itself.

</div>

<div class="feature-section" id="convert-mnemonics">

## convert-mnemonics

**Purpose**: Keyboard mnemonic handling improvements.

**Role**: Enhanced keyboard accessibility and shortcuts.

**Files Modified**:
- `libgimp/gimpproceduredialog.c`

**Implementation**: Improves keyboard mnemonic handling for better accessibility and keyboard navigation.

</div>

<div class="feature-section" id="convert-tool-events">

## convert-tool-events

**Purpose**: Tool event handling system enhancement with device-aware input processing, improved layer picking, and coordinate handling for tool responsiveness.

**Role**: Core input system improvement that provides better device support, layer interaction, and improved tool event processing for superior user experience.

**Files Modified** (4 files, 160 insertions, 13 deletions):
- `app/display/gimpdisplayshell-tool-events.c` (136 insertions, 2 deletions): Major tool event handling enhancement with device awareness and layer picking
- `app/display/gimpdisplayshell.c` (4 insertions): Display shell integration improvements
- `app/display/gimpdisplayshell.h` (9 insertions): Enhanced interface declarations and coordinate handling
- `app/widgets/gimpdeviceinfo-coords.c` (24 insertions, 11 deletions): Improved device coordinate processing

**Implementation**: This branch implements improvements to tool event handling:

1. **Input Device Support**: Adds device awareness with `GdkInputSource` detection and `GdkDevice` integration:
   - Device change detection for better tablet/stylus support
   - Input source awareness for different device types
   - Device coordinate processing

2. **Layer Picking System**: Introduces `set_picked_layer()` function with duration-based layer selection:
   - Layer picking with configurable handle duration
   - Improved layer interaction workflows
   - Better support for complex layer hierarchies

3. **Tool Integration Enhancements**: Expands tool integration with additional tool type support:
   - Transform tool integration (`gimptransformtool.h`)
   - Tool info integration (`core/gimptoolinfo.h`)
   - Tool control and management

4. **Default Coordinate System**: Implements `GIMP_COORDS_DEFAULT_VALUES` for consistent coordinate initialization and better coordinate handling throughout the event system.

5. **Event Processing**: Improved event processing pipeline with better device change detection, coordinate validation, and tool responsiveness.

This enhancement provides the foundation for input handling, particularly beneficial for digital artists using tablets, styluses, and other input devices with Artbox.

</div>

<div class="feature-section" id="convert-localization-messaging">

## convert-localization-messaging

**Purpose**: Suppresses plugin localization error messages that can clutter the console when translation directories are missing.

**Role**: Reduces console noise from localization warnings while maintaining functional localization where directories exist.

**Files Modified**:
- `libgimp/gimpplugin.c` (5 lines modified - 5 deletions)

**Implementation**: Comments out three specific `g_printerr()` calls in the `_gimp_plug_in_set_i18n()` function that warn about missing translation catalog directories. These messages typically appear when:
- Plugin translation directories don't exist
- Plugins haven't implemented custom localization
- Default localization paths are unavailable

The warnings provided limited value to end users while creating console clutter, especially during plugin development or when using plugins without full translation support. The actual localization functionality remains intact - only the warning output is suppressed.

</div>

<div class="feature-section" id="convert-broken-pipe">

## convert-broken-pipe

**Purpose**: Suppresses flush error warning messages that can spam the console during plugin communication failures.

**Role**: Reduces console noise by disabling specific warning messages related to plugin communication errors.

**Files Modified**:
- `libgimp/gimpplugin.c` (6 lines modified - 3 insertions, 3 deletions)

**Implementation**: Comments out two specific `g_warning()` calls in the `gimp_plug_in_flush()` function that report communication errors between GIMP core and plugins. These warnings can become excessive when plugins crash or disconnect, flooding the console with repetitive error messages. The actual error handling and recovery mechanisms remain intact - only the warning output is suppressed to provide a cleaner user experience.

</div>

<div class="feature-section" id="convert-display-options">

## convert-display-options

**Purpose**: Display enhancement introducing selection highlighting system with user-configurable visibility controls and view menu integration.

**Role**: Visual system enhancement that provides selection visualization capabilities with user interface integration and customization options.

**Files Modified** (8 files, 92 insertions):
- `app/actions/view-actions.c` (9 insertions): New view action for selection highlight toggle with menu integration
- `app/actions/view-commands.c` (18 insertions): Command implementation for selection highlight toggle functionality
- `app/actions/view-commands.h` (3 insertions): Command function declarations for selection highlight
- `app/config/gimpdisplayoptions.c` (28 insertions): Display options configuration for selection highlighting
- `app/config/gimpdisplayoptions.h` (1 insertion): Display options structure enhancement
- `app/display/gimpdisplayshell-appearance.c` (26 insertions): Display shell appearance handling for highlighting
- `app/display/gimpdisplayshell-appearance.h` (6 insertions): Appearance function declarations
- `menus/image-menu.ui.in.in` (1 insertion): View menu integration for selection highlight toggle

**Implementation**: This branch introduces a selection highlighting system:

1. **Selection Highlight Toggle Action**: Adds `view-show-selection-highlight` action that allows users to toggle selection highlighting on/off through the View menu:
   ```c
   { "view-show-selection-highlight", NULL,
     NC_("view-action", "Show Selection _Highlight"), NULL, { NULL },
     NC_("view-action", "Show the tinted selection highlighting"),
     view_toggle_selection_highlight_cmd_callback, TRUE, GIMP_HELP_VIEW_SHOW_SELECTION }
   ```

2. **Command Integration**: Implements `view_toggle_selection_highlight_cmd_callback()` function that integrates with the display shell to provide real-time toggling of selection highlighting.

3. **Configuration System Integration**: Extends `gimpdisplayoptions` with `show_selection_highlight` property, allowing the highlighting preference to be saved and restored across sessions.

4. **Display Shell Integration**: Enhances the display shell appearance system with selection highlighting rendering capabilities, providing smooth integration with existing display features.

5. **Menu System Integration**: Adds the selection highlight toggle to the View menu, making it easily accessible to users alongside other display options.

This enhancement provides users with control over selection visualization, supporting both minimal interfaces for experienced users and visual feedback for complex selection workflows.

</div>

<div class="feature-section" id="convert-supress-timer-prints">

## convert-supress-timer-prints

**Purpose**: Development experience enhancement that suppresses performance timing debug output to reduce console noise while maintaining timing functionality for development use.

**Role**: Debug output management that provides cleaner console output for end users while preserving timing capabilities for development and profiling scenarios.

**Files Modified** (1 file, 5 insertions, 3 deletions):
- `app/core/gimp-utils.h` (8 lines modified): Timer print suppression in GIMP_TIMER_END macro

**Implementation**: This branch improves the development and user experience by suppressing debug timing output:

1. **Timer Print Suppression**: Comments out the `g_printerr()` call in the `GIMP_TIMER_END` macro that outputs performance timing information:
   ```c
   /* g_printerr ("%s: %s took %0.4f seconds\n", \
                    G_STRFUNC, message,           \
                    g_timer_elapsed (_timer, NULL)); */
   ```

2. **Preserved Functionality**: Maintains the complete timer infrastructure including timer creation, measurement, and destruction - only the console output is suppressed.

3. **Clean Console Output**: Eliminates performance timing messages that could clutter the console during normal application use, providing a cleaner user experience.

4. **Development Flexibility**: The commented-out code can be easily re-enabled for development, profiling, or debugging scenarios by uncommenting the print statements.

5. **Timer Resource Management**: Preserves proper timer cleanup with `g_timer_destroy(_timer)` to prevent memory leaks.

This change supports Artbox's focus on providing a user experience by reducing debug output noise while maintaining the underlying performance measurement infrastructure for development purposes.

</div>

<div class="feature-section" id="convert-brush-preview">

## convert-brush-preview

**Purpose**: Brush preview system enhancement that enables theme-following viewables by default while providing users control over theme integration for improved visual consistency.

**Role**: User interface improvement that provides better default brush preview behavior while maintaining user customization options for workflows.

**Files Modified** (2 files, 2 insertions, 2 deletions):
- `app/config/gimpguiconfig.c` (1 insertion, 1 deletion): Changed viewables follow theme default from FALSE to TRUE
- `app/widgets/gimpbrushfactoryview.c` (1 insertion, 1 deletion): Changed follow theme toggle display from TRUE to FALSE

**Implementation**: This branch implements complementary changes that improve the brush preview experience:

1. **Default Theme Following Enabled**: Changes the default value for `viewables-follow-theme` from `FALSE` to `TRUE`:
   - **Benefit**: Brush previews now automatically adapt to the application theme by default
   - **Impact**: Provides better visual consistency between the interface and brush previews
   - **User Experience**: New users get a more cohesive visual experience without manual configuration

2. **Simplified Factory View Interface**: Changes the follow theme toggle display in brush factory view from `TRUE` to `FALSE`:
   - **Result**: Reduces interface clutter by hiding the theme toggle control by default
   - **Rationale**: Since theme following is now enabled by default, most users won't need to access this control
   - **Advanced Access**: The functionality remains available through preferences for users who need custom control

3. **Improved Default Workflow**: The combination of these changes provides:
   - Theme-consistent brush previews out of the box
   - Cleaner brush selection interface
   - Reduced need for manual configuration

This enhancement aligns with Artbox's philosophy of providing sensible defaults that work well for most users while maintaining customization capabilities for workflows.

</div>

<div class="feature-section" id="convert-commands-dockable">

## convert-commands-dockable

**Purpose**: Commands Dockable implementation providing a visual grid interface for custom commands and plugins with dual-language execution support (Script-Fu and Python).

**Role**: Core scripting and automation infrastructure that enables users to create, store, and execute custom commands through a visual macro palette interface.

**Files Modified** (65 files, extensive additions):

**Core Implementation**:
- `app/core/gimpcommanditem.c` (new file): Complete GimpCommandItem data class with GimpConfig serialization
- `app/core/gimpcommanditem.h` (new file): Command item class declarations and property definitions
- `app/core/gimpcommanditem-load.c` (new file): .gcmd file loading implementation
- `app/core/gimpcontext.c` (additions): Command item context integration with change notifications

**Widget System**:
- `app/widgets/gimpcommandeditor.c` (new file): Command editor widget with name entry, text view, description, and icon picker
- `app/widgets/gimpcommandview.c` (new file): Individual command view with hover states and icon caching
- `app/widgets/gimpcommandfactoryview.c` (new file): Factory view with grid layout and item-hovered signals
- `app/widgets/gimpcommandcontainerview.c` (new file): Container view for command item management
- `app/widgets/gimpcommandutils.c` (new file): Language-specific execution utilities with error handling

**Action System**:
- `app/actions/command-actions.c` (new file): Action group with new/duplicate/save/execute/delete operations
- `app/actions/command-commands.c` (new file): Command operation callback implementations
- `app/actions/command-editor-actions.c` (new file): Editor-specific action system
- `app/actions/command-editor-commands.c` (new file): Editor command implementations

**Configuration & Integration**:
- `app/config/gimpcoreconfig.c` (additions): Command path configuration properties
- `app/core/gimp-data-factories.c` (additions): Command factory initialization and cleanup
- `app/dialogs/dialogs-constructors.c` (additions): Commands dialog constructor
- `menus/commands-menu.ui` (new file): Commands dialog context menu
- `menus/command-editor-menu.ui` (new file): Command editor context menu

**Data Files**:
- `data/commands/Hello-World.gcmd`: Script-Fu hello world example
- `data/commands/Hello-Python-World.gcmd`: Python hello world example  
- `data/commands/Guide-Fifths.gcmd`: Guide creation command
- `data/commands/Python-Document-Info.gcmd`: Python document information command

**Implementation**: This branch introduces a comprehensive command management system:

1. **Dual-Language Execution**: Commands support both Script-Fu and Python through language-specific PDB eval procedures:
   - Script-Fu commands use `plug-in-script-fu-eval`
   - Python commands use `python-fu-eval`
   - Language detection and routing with comprehensive error handling

2. **Visual Grid Interface**: Factory view displays commands as clickable icons in a grid layout, providing a visual macro palette that replaces complex keyboard shortcuts with single-click access.

3. **File Format Support**: .gcmd (GIMP Command) file format with GimpConfig serialization:
   ```
   # GIMP command item
   (name "Command Name")
   (command "script content")
   (description "Description")
   (language script-fu|python)
   # end of GIMP command item
   ```

4. **Command Lifecycle Management**: Complete CRUD operations for command items:
   - **Creation**: New empty commands with default properties
   - **Duplication**: Clone existing commands for modification
   - **Persistence**: Save commands to user and system directories
   - **Execution**: Run commands through appropriate language interpreter
   - **Deletion**: Remove commands with confirmation dialogs

5. **UI Integration**: Full integration with GIMP's dialog and menu systems:
   - Accessible through Windows > Dockable Dialogs > Commands
   - Context menus for command operations
   - Editor interface with metadata management
   - Hover states and visual feedback

6. **Resource Management**: Integration with GIMP's data factory system:
   - Commands stored in `~/.config/GIMP/commands/` (user) and application data directory (system)
   - Auto-loading on GIMP startup
   - Resource container integration for standard GIMP workflows

This implementation transforms the way users interact with GIMP automation, providing a visual alternative to complex scripting workflows and enabling rapid access to frequently used operations through an intuitive grid interface.

</div>

<div class="feature-section" id="convert-gitlab-ci">

## convert-gitlab-ci

**Purpose**: GitLab CI/CD pipeline infrastructure for Artbox AppImage generation and distribution.

**Role**: Provides automated build, packaging, and deployment system for Artbox, including AppImage creation infrastructure.

**Files Modified** (27 files, 2,993 insertions, 13 deletions):
- `app/gimp-version.c` (4 modifications - version identification)
- `build/linux/appimage/README-CI.md` (897 lines - comprehensive CI documentation)
- `build/linux/appimage/artbox-goappimage.sh` (108 lines - main AppImage build script)
- `build/linux/appimage/docker/deps.Dockerfile` (45 lines - Docker dependency setup)
- `build/linux/appimage/lib/bundling/core.sh` (136 lines - core bundling logic)
- `build/linux/appimage/lib/bundling/extras.sh` (77 lines - extra components)
- `build/linux/appimage/lib/bundling/finalize.sh` (108 lines - build finalization)
- `build/linux/appimage/lib/bundling/main.sh` (65 lines - main bundling coordination)
- `build/linux/appimage/lib/bundling/plugins.sh` (47 lines - plugin handling)
- `build/linux/appimage/lib/bundling/resources.sh` (132 lines - resource management)
- `build/linux/appimage/lib/bundling/utilities.sh` (298 lines - utility functions)
- `build/linux/appimage/lib/config/arguments.sh` (53 lines - argument parsing)
- `build/linux/appimage/lib/config/environment.sh` (76 lines - environment setup)
- `build/linux/appimage/lib/config/identity.sh` (49 lines - identity configuration)
- `build/linux/appimage/lib/config/main.sh` (16 lines - main configuration)
- `build/linux/appimage/lib/config/paths.sh` (40 lines - path management)
- `build/linux/appimage/lib/logging.sh` (455 lines - comprehensive logging system)
- `build/linux/appimage/lib/packaging/appimage.sh` (139 lines - AppImage packaging)
- `build/linux/appimage/lib/tools/dependencies.sh` (126 lines - dependency management)
- `data/artbox-release.in` (2 lines - release information)
- `data/desktop-integration-README.md` (72 lines - desktop integration guide)
- `data/meson.build` (38 modifications - build system updates)
- `desktop/artbox.desktop.in.in` (7 lines - Artbox desktop entry)
- `desktop/gimp.desktop.in.in` (2 modifications - GIMP desktop entry updates)
- `desktop/meson.build` (2 modifications - desktop build configuration)
- `libgimpwidgets/gimpwidgets-private.c` (10 modifications - widget system updates)
- `meson.build` (2 modifications - main build configuration)

**Implementation**: Infrastructure addition that creates a CI/CD pipeline for Artbox. The system includes modular bash libraries for AppImage creation, logging infrastructure, Docker-based dependency management, and automated packaging workflows. This branch transforms the project from a simple GIMP fork into a packaged application with automated distribution capabilities.

</div>
