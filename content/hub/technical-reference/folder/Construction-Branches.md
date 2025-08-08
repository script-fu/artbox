---
type: docs
url: "hub/technical-reference/folder/Construction-Branches"
---

# Construction Branches

All branches used in the Artbox staged construction pipeline, organized alphabetically. These branches are processed through numbered stages (01, 015, 02, 03, 04, 05, 06) to build the final Artbox application.

## Branch Overview

{{< cards >}}
  {{< card link="#additional-script-fu-pdb" title="additional-script-fu-pdb" subtitle="Stage 05 - Additional Script-Fu PDB functionality" >}}
  {{< card link="#alt-layer-picking" title="alt-layer-picking" subtitle="Stage 04 - Alt-click layer selection" >}}
  {{< card link="#artbox-name-branding" title="artbox-name-branding" subtitle="Stage 04 - Artbox branding and naming" >}}
  {{< card link="#brush-aspect-ratio" title="brush-aspect-ratio" subtitle="Stage 04 - Brush aspect ratio controls" >}}
  {{< card link="#brush-motion-processing" title="brush-motion-processing" subtitle="Stage 06 - Motion buffer for smooth strokes" >}}
  {{< card link="#brush-preview-false" title="brush-preview-false" subtitle="Stage 03 - Brush preview disabled by default" >}}
  {{< card link="#colour-picker-sample-merged-alt" title="colour-picker-sample-merged-alt" subtitle="Stage 05 - Color picker sample merged Alt functionality" >}}
  {{< card link="#commands-dockable-signals" title="commands-dockable-signals" subtitle="Stage 03 - Commands dockable signal implementation" >}}
  {{< card link="#curve-view-enhanced" title="curve-view-enhanced" subtitle="Stage 04 - Enhanced curve view interface" >}}
  {{< card link="#dialogs-editor-icons" title="dialogs-editor-icons" subtitle="Stage 04 - Dialog editor icons" >}}
  {{< card link="#display-options-extended" title="display-options-extended" subtitle="Stage 04 - Extended display options" >}}
  {{< card link="#duplicate-layer-and-clear" title="duplicate-layer-and-clear" subtitle="Stage 03 - Layer duplication and clearing" >}}
  {{< card link="#dynamic-brush-spacing" title="dynamic-brush-spacing" subtitle="Stage 03 - Dynamic brush spacing control" >}}
  {{< card link="#dynamics-editor-enhanced" title="dynamics-editor-enhanced" subtitle="Stage 04 - Enhanced dynamics editor" >}}
  {{< card link="#eraser-on-masks" title="eraser-on-masks" subtitle="Stage 05 - Enhanced eraser functionality on masks" >}}
  {{< card link="#filter-restores-previous-tool" title="filter-restores-previous-tool" subtitle="Stage 05 - Filter operations restore previous tool" >}}
  {{< card link="#force-artbox-config" title="force-artbox-config" subtitle="Stage 04 - Force Artbox configuration" >}}
  {{< card link="#free-selection-fill" title="free-selection-fill" subtitle="Stage 05 - Free selection fill functionality" >}}
  {{< card link="#fullscreen-is-fullscreen" title="fullscreen-is-fullscreen" subtitle="Stage 05 - True fullscreen mode" >}}
  {{< card link="#gfig-tweak" title="gfig-tweak" subtitle="Stage 05 - GFig plugin improvements" >}}
  {{< card link="#gimpconfig-path-extend" title="gimpconfig-path-extend" subtitle="Stage 04 - Extended configuration path handling" >}}
  {{< card link="#gimpcontext-changes" title="gimpcontext-changes" subtitle="Stage 04 - Context system changes" >}}
  {{< card link="#gimpdynamicsoutput" title="gimpdynamicsoutput" subtitle="Stage 05 - Dynamics output enhancements" >}}
  {{< card link="#gimpgrouplayer-functions" title="gimpgrouplayer-functions" subtitle="Stage 04 - Group layer functions" >}}
  {{< card link="#gimpicons-extended" title="gimpicons-extended" subtitle="Stage 04 - Extended icon set" >}}
  {{< card link="#gimpimage-functions" title="gimpimage-functions" subtitle="Stage 04 - Image functions" >}}
  {{< card link="#gimpitem-functions" title="gimpitem-functions" subtitle="Stage 02 - Item functions" >}}
  {{< card link="#gimppickable-auto-shrink-bg-color" title="gimppickable-auto-shrink-bg-color" subtitle="Stage 04 - Auto-shrink background color" >}}
  {{< card link="#gitlab-ci-artbox-scripts" title="gitlab-ci-artbox-scripts" subtitle="Stage 04 - GitLab CI scripts for Artbox" >}}
  {{< card link="#gui-size-tweaks" title="gui-size-tweaks" subtitle="Stage 05 - GUI size adjustments" >}}
  {{< card link="#gui-style-settings" title="gui-style-settings" subtitle="Stage 05 - Style and theme settings" >}}
  {{< card link="#help-id-path-edit" title="help-id-path-edit" subtitle="Stage 04 - Help ID path editing" >}}
  {{< card link="#icon-picker-enhanced" title="icon-picker-enhanced" subtitle="Stage 01 - Enhanced icon picker functionality" >}}
  {{< card link="#initial-commands-dockable" title="initial-commands-dockable" subtitle="Stage 015 - Initial commands dockable implementation" >}}
  {{< card link="#issue-templates-artbox" title="issue-templates-artbox" subtitle="Stage 04 - Artbox issue templates" >}}
  {{< card link="#jitter-distribution-option" title="jitter-distribution-option" subtitle="Stage 05 - Brush jitter distribution options" >}}
  {{< card link="#layer-pop-up-menu" title="layer-pop-up-menu" subtitle="Stage 01 - Layer context menu enhancements" >}}
  {{< card link="#max-brush-size" title="max-brush-size" subtitle="Stage 05 - Maximum brush size adjustments" >}}
  {{< card link="#meson-for-artbox-resources" title="meson-for-artbox-resources" subtitle="Stage 01 - Meson build system for Artbox resources" >}}
  {{< card link="#paintbrush-high-quality-force" title="paintbrush-high-quality-force" subtitle="Stage 05 - High-quality paintbrush rendering enforcement" >}}
  {{< card link="#paintbrush-options-artbox" title="paintbrush-options-artbox" subtitle="Stage 02 - Artbox-specific paintbrush options" >}}
  {{< card link="#painttool-cursor" title="painttool-cursor" subtitle="Stage 05 - Paint tool cursor enhancements" >}}
  {{< card link="#path-editing" title="path-editing" subtitle="Stage 05 - Path editing tools" >}}
  {{< card link="#path-snapping" title="path-snapping" subtitle="Stage 05 - Enhanced path snapping functionality" >}}
  {{< card link="#preferences-dialog" title="preferences-dialog" subtitle="Stage 01 - Preferences dialog enhancements" >}}
  {{< card link="#presets-doubleclick-restore" title="presets-doubleclick-restore" subtitle="Stage 05 - Tool preset double-click restoration" >}}
  {{< card link="#recent-layer-mode-group" title="recent-layer-mode-group" subtitle="Stage 05 - Recent layer mode grouping" >}}
  {{< card link="#resource-control" title="resource-control" subtitle="Stage 05 - Resource management with save-as functionality" >}}
  {{< card link="#resource-filtering-option" title="resource-filtering-option" subtitle="Stage 05 - Resource filtering options" >}}
  {{< card link="#script-fu-autostart" title="script-fu-autostart" subtitle="Stage 04 - Script-Fu autostart functionality" >}}
  {{< card link="#script-fu-plugins-for-artbox" title="script-fu-plugins-for-artbox" subtitle="Stage 05 - Custom Script-Fu plugins for Artbox" >}}
  {{< card link="#selection-highlight" title="selection-highlight" subtitle="Stage 03 - Selection highlighting enhancements" >}}
  {{< card link="#simple-sliders" title="simple-sliders" subtitle="Stage 05 - Simplified slider interface" >}}
  {{< card link="#smooth-stroke" title="smooth-stroke" subtitle="Stage 05 - Stroke smoothing" >}}
  {{< card link="#stability-bug-fixes" title="stability-bug-fixes" subtitle="Stage 02 - Stability and bug fixes" >}}
  {{< card link="#status-bar-for-artbox" title="status-bar-for-artbox" subtitle="Stage 05 - Status bar enhancements" >}}
  {{< card link="#supress-broken-pipe-warnings" title="supress-broken-pipe-warnings" subtitle="Stage 04 - Suppress broken pipe warnings" >}}
  {{< card link="#supress-localization-warnings" title="supress-localization-warnings" subtitle="Stage 01 - Suppress localization warnings" >}}
  {{< card link="#supress-mnemonics-warnings" title="supress-mnemonics-warnings" subtitle="Stage 01 - Suppress mnemonics warnings" >}}
  {{< card link="#supress-paintbrush-slider-tool-tips" title="supress-paintbrush-slider-tool-tips" subtitle="Stage 05 - Suppress paintbrush slider tooltips" >}}
  {{< card link="#supress-timer-printout" title="supress-timer-printout" subtitle="Stage 04 - Suppress timer printouts" >}}
  {{< card link="#supress-warning-messages" title="supress-warning-messages" subtitle="Stage 01 - Warning message suppression" >}}
  {{< card link="#tool-preset-structure" title="tool-preset-structure" subtitle="Stage 02 - Tool preset data structures" >}}
  {{< card link="#tool-tips-hacked-out" title="tool-tips-hacked-out" subtitle="Stage 04 - Tooltip removal" >}}
  {{< card link="#toolbox-flexible-refactor" title="toolbox-flexible-refactor" subtitle="Stage 05 - Flexible toolbox refactor" >}}
  {{< card link="#transform-tool-use-selection" title="transform-tool-use-selection" subtitle="Stage 05 - Transform tool selection usage" >}}
  {{< card link="#warp-tool-for-artbox" title="warp-tool-for-artbox" subtitle="Stage 05 - Warp tool enhancements for Artbox" >}}
{{< /cards >}}

---

<div class="feature-section" id="additional-script-fu-pdb">

## additional-script-fu-pdb

**Stage**: 05
**Description**: Extends the Script-Fu Procedure Database with additional procedures for Artbox workflows</div>

<div class="feature-section" id="alt-layer-picking">

## alt-layer-picking

**Stage**: 04
**Description**: Enables Alt+click to select layers directly from the canvas</div>

<div class="feature-section" id="artbox-name-branding">

## artbox-name-branding

**Stage**: 04
**Description**: Updates application strings, titles, and branding elements throughout the interface to reflect Artbox identity</div>

<div class="feature-section" id="brush-aspect-ratio">

## brush-aspect-ratio

**Stage**: 04
**Description**: Adds brush aspect ratio adjustment capabilities to the paint system</div>

<div class="feature-section" id="brush-motion-processing">

## brush-motion-processing

**Stage**: 06
**Description**: Implements motion processing buffer for smoother brush stroke rendering</div>

<div class="feature-section" id="brush-preview-false">

## brush-preview-false

**Stage**: 03
**Description**: Sets brush preview to false by default to improve painting performance</div>

<div class="feature-section" id="colour-picker-sample-merged-alt">

## colour-picker-sample-merged-alt

**Stage**: 05
**Description**: Enhanced color picker with Alt-key sample merged behavior</div>

<div class="feature-section" id="commands-dockable-signals">

## commands-dockable-signals

**Stage**: 03
**Description**: Implements signal handling for the commands dockable interface

</div>

<div class="feature-section" id="curve-view-enhanced">

## curve-view-enhanced

**Stage**: 04
**Description**: Improvements to the curve editing interface for better usability

</div>

<div class="feature-section" id="dialogs-editor-icons">

## dialogs-editor-icons

**Stage**: 04
**Description**: Updates and enhances icons used in dialog editors

</div>

<div class="feature-section" id="display-options-extended">

## display-options-extended

**Stage**: 04
**Description**: Adds additional display configuration options for Artbox

</div>

<div class="feature-section" id="duplicate-layer-and-clear">

## duplicate-layer-and-clear

**Stage**: 03
**Description**: Enhanced layer operations for duplicating and clearing layer content</div>

<div class="feature-section" id="dynamic-brush-spacing">

## dynamic-brush-spacing

**Stage**: 03
**Description**: Implements dynamic spacing adjustments for brush strokes that respond to input pressure, velocity, and other dynamics parameters

**Files Modified** (6 files, 148 insertions, 22 deletions):
- `app/core/gimpdynamics.c` (64 lines modified): Core dynamics system changes
- `app/paint/gimpbrushcore.c` (60 lines modified): Brush core spacing implementation
- `app/paint/gimpbrushcore.h` (15 lines modified): Header definitions
- `app/paint/gimppaintcore.c` (18 lines modified): Paint core integration
- `app/paint/gimppaintcore.h` (8 lines modified): Paint core headers
- `app/tools/gimppaintoptions-gui.c` (5 lines modified): GUI option controls

**Implementation**: This branch was a proposed solution to https://gitlab.gnome.org/GNOME/gimp/-/issues/1863, implementing dynamic brush spacing that responds to input pressure, velocity, and other dynamics parameters for more natural brush behavior.</div>

<div class="feature-section" id="dynamics-editor-enhanced">

## dynamics-editor-enhanced

**Stage**: 04
**Description**: Improvements to the dynamics editor for better workflow and usability

</div>

<div class="feature-section" id="eraser-on-masks">

## eraser-on-masks

**Stage**: 05
**Description**: Improves eraser tool behavior when working with layer masks

</div>

<div class="feature-section" id="filter-restores-previous-tool">

## filter-restores-previous-tool

**Stage**: 05
**Description**: Automatically restores the previously selected tool after running filters

</div>

<div class="feature-section" id="force-artbox-config">

## force-artbox-config

**Stage**: 04
**Description**: Ensures Artbox-specific configuration is properly applied and maintained

</div>

<div class="feature-section" id="free-selection-fill">

## free-selection-fill

**Stage**: 05
**Description**: Enhanced fill operations for free selection tools

</div>

<div class="feature-section" id="fullscreen-is-fullscreen">

## fullscreen-is-fullscreen

**Stage**: 05
**Description**: Ensures fullscreen mode properly hides all interface elements for distraction-free work</div>

<div class="feature-section" id="gfig-tweak">

## gfig-tweak

**Stage**: 05
**Description**: Enhancements and fixes to the GFig geometric figure plugin

</div>

<div class="feature-section" id="gimpconfig-path-extend">

## gimpconfig-path-extend

**Stage**: 04
**Description**: Extends configuration system path handling capabilities

</div>

<div class="feature-section" id="gimpcontext-changes">

## gimpcontext-changes

**Stage**: 04
**Description**: Modifications to GIMP's context management system for Artbox

</div>

<div class="feature-section" id="gimpdynamicsoutput">

## gimpdynamicsoutput

**Stage**: 05
**Description**: Improvements to dynamics output processing and behavior

</div>

<div class="feature-section" id="gimpgrouplayer-functions">

## gimpgrouplayer-functions

**Stage**: 04
**Description**: Enhanced functionality for group layer operations

</div>

<div class="feature-section" id="gimpicons-extended">

## gimpicons-extended

**Stage**: 04
**Description**: Adds additional icons and icon resources for Artbox interface

</div>

<div class="feature-section" id="gimpimage-functions">

## gimpimage-functions

**Stage**: 04
**Description**: Additional and enhanced image manipulation functions

</div>

<div class="feature-section" id="gimpitem-functions">

## gimpitem-functions

**Stage**: 02
**Description**: Core functionality extensions for GIMP item operations

</div>

<div class="feature-section" id="gimppickable-auto-shrink-bg-color">

## gimppickable-auto-shrink-bg-color

**Stage**: 04
**Description**: Automatic background color handling for pickable objects</div>

<div class="feature-section" id="gitlab-ci-artbox-scripts">

## gitlab-ci-artbox-scripts

**Stage**: 04
**Description**: Continuous integration scripts specific to Artbox development and deployment

</div>

<div class="feature-section" id="gui-size-tweaks">

## gui-size-tweaks

**Stage**: 05
**Description**: Fine-tuning of interface element sizes for improved user experience

</div>

<div class="feature-section" id="gui-style-settings">

## gui-style-settings

**Stage**: 05
**Description**: Custom styling and theming options for the Artbox interface

</div>

<div class="feature-section" id="help-id-path-edit">

## help-id-path-edit

**Stage**: 04
**Description**: Modifications to help system path handling and ID management

</div>

<div class="feature-section" id="icon-picker-enhanced">

## icon-picker-enhanced

**Stage**: 01
**Description**: Improved icon selection and management interface

</div>

<div class="feature-section" id="initial-commands-dockable">

## initial-commands-dockable

**Stage**: 015
**Description**: Foundation implementation for the commands dockable interface

</div>

<div class="feature-section" id="issue-templates-artbox">

## issue-templates-artbox

**Stage**: 04
**Description**: Custom issue templates for Artbox development and bug reporting

</div>

<div class="feature-section" id="jitter-distribution-option">

## jitter-distribution-option

**Stage**: 05
**Description**: Enhanced jitter distribution controls for more natural brush behavior

</div>

<div class="feature-section" id="layer-pop-up-menu">

## layer-pop-up-menu

**Stage**: 01
**Description**: Improved right-click context menu for layer operations

</div>

<div class="feature-section" id="max-brush-size">

## max-brush-size

**Stage**: 05
**Description**: Increases maximum allowable brush size for large canvas work

</div>

<div class="feature-section" id="meson-for-artbox-resources">

## meson-for-artbox-resources

**Stage**: 01
**Description**: Build system configuration for Artbox-specific resources and assets</div>

<div class="feature-section" id="paintbrush-high-quality-force">

## paintbrush-high-quality-force

**Stage**: 05
**Description**: Memory safety improvements and high-quality paintbrush rendering with enhanced buffer allocation and integer overflow protection

**Files Modified** (2 files, 78 insertions, 50 deletions):
- `app/core/gimptempbuf.c` (97 lines modified): Enhanced buffer allocation with overflow protection
- `app/paint/gimpbrushcore-loops.cc` (31 lines modified): Updated brush rendering loops for high-quality force operations

**Implementation**: Implements safety and quality improvements including integer overflow protection, memory safety, improved buffer creation, and high-quality force activation for better paintbrush stability and quality.</div>

<div class="feature-section" id="paintbrush-options-artbox">

## paintbrush-options-artbox

**Stage**: 02
**Description**: Custom paintbrush configuration and options tailored for Artbox workflows

</div>

<div class="feature-section" id="painttool-cursor">

## painttool-cursor

**Stage**: 05
**Description**: Improved cursor display and behavior for paint tools

</div>

<div class="feature-section" id="path-editing">

## path-editing

**Stage**: 05
**Description**: Enhanced path creation, editing, and manipulation tools

</div>

<div class="feature-section" id="path-snapping">

## path-snapping

**Stage**: 05
**Description**: Improved snapping behavior for path tools and operations

</div>

<div class="feature-section" id="preferences-dialog">

## preferences-dialog

**Stage**: 01
**Description**: Improvements and additions to the preferences interface</div>

<div class="feature-section" id="presets-doubleclick-restore">

## presets-doubleclick-restore

**Stage**: 05
**Description**: Double-click functionality to restore preset settings without requiring preset switching

**Files Modified** (1 file, 3 insertions):
- `app/widgets/gimpcontainericonview.c` (3 lines added): Double-click restoration functionality

**Implementation**: Adds workflow enhancement where double-clicking an already active preset restores the tool options to the preset's saved state, eliminating the need to switch presets to restore settings.</div>

<div class="feature-section" id="recent-layer-mode-group">

## recent-layer-mode-group

**Stage**: 05
**Description**: Groups recently used layer blend modes for easier access

</div>

<div class="feature-section" id="resource-control">

## resource-control

**Stage**: 05
**Description**: Enhanced resource management including save-as operations for brushes, patterns, and other resources

</div>

<div class="feature-section" id="resource-filtering-option">

## resource-filtering-option

**Stage**: 05
**Description**: Advanced filtering capabilities for resource browsers and selectors

</div>

<div class="feature-section" id="script-fu-autostart">

## script-fu-autostart

**Stage**: 04
**Description**: Automatic startup of Script-Fu scripts for Artbox workflows</div>

<div class="feature-section" id="script-fu-plugins-for-artbox">

## script-fu-plugins-for-artbox

**Stage**: 05
**Description**: Collection of 20 custom plugins with workflow automation (9,008 lines of code)

### Plugin Categories:
- **Paint Tool Utilities**: Brush and painting workflow enhancements
- **Layer Management**: Advanced layer operations and organization
- **File Management**: File handling and batch operations
- **Effects & Utilities**: Various utility functions and effects</div>

<div class="feature-section" id="selection-highlight">

## selection-highlight

**Stage**: 03
**Description**: Improved visual feedback for selections with enhanced highlighting

</div>

<div class="feature-section" id="simple-sliders">

## simple-sliders

**Stage**: 05
**Description**: Streamlined slider controls for better user experience

</div>

<div class="feature-section" id="smooth-stroke">

## smooth-stroke

**Stage**: 05
**Description**: Stroke stabilization and smoothing for cleaner brush strokes

</div>

<div class="feature-section" id="stability-bug-fixes">

## stability-bug-fixes

**Stage**: 02
**Description**: Various stability enhancements and bug fixes for improved reliability

</div>

<div class="feature-section" id="status-bar-for-artbox">

## status-bar-for-artbox

**Stage**: 05
**Description**: Custom status bar information and display for Artbox workflows</div>

<div class="feature-section" id="supress-broken-pipe-warnings">

## supress-broken-pipe-warnings

**Stage**: 04
**Description**: Reduces console noise by suppressing broken pipe warnings

</div>

<div class="feature-section" id="supress-localization-warnings">

## supress-localization-warnings

**Stage**: 01
**Description**: Reduces console output by suppressing localization-related warnings

</div>

<div class="feature-section" id="supress-mnemonics-warnings">

## supress-mnemonics-warnings

**Stage**: 01
**Description**: Reduces console noise by suppressing mnemonic-related warnings

</div>

<div class="feature-section" id="supress-paintbrush-slider-tool-tips">

## supress-paintbrush-slider-tool-tips

**Stage**: 05
**Description**: Removes tooltips from paintbrush sliders for cleaner interface

</div>

<div class="feature-section" id="supress-timer-printout">

## supress-timer-printout

**Stage**: 04
**Description**: Reduces console output by suppressing timing debug messages

</div>

<div class="feature-section" id="supress-warning-messages">

## supress-warning-messages

**Stage**: 01
**Description**: Reduces console noise by suppressing various warning messages</div>

<div class="feature-section" id="tool-preset-structure">

## tool-preset-structure

**Stage**: 02
**Description**: Foundation data structures and handling for tool presets that other branches depend on

**Files Modified**: Core tool preset system files
**Implementation**: Provides data structures and handling for tool presets that other branches depend on. Expands tool preset functionality with new code for preset management, device integration, and preset editor enhancements.

</div>

<div class="feature-section" id="tool-tips-hacked-out">

## tool-tips-hacked-out

**Stage**: 04
**Description**: Removes tooltips from various interface elements to reduce visual clutter

</div>

<div class="feature-section" id="toolbox-flexible-refactor">

## toolbox-flexible-refactor

**Stage**: 05
**Description**: Major toolbox interface restructuring for improved flexibility and usability

</div>

<div class="feature-section" id="transform-tool-use-selection">

## transform-tool-use-selection

**Stage**: 05
**Description**: Improved transform tool behavior when working with selections

</div>

<div class="feature-section" id="warp-tool-for-artbox">

## warp-tool-for-artbox

**Stage**: 05
**Description**: Custom warp tool modifications and improvements for Artbox use cases

</div>
