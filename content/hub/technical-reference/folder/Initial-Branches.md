---
type: docs
url: "hub/technical-reference/folder/Initial-Branches"
---

# Initial Branches

Foundation branches that prepare GIMP source and provide essential utilities for other branches.

## Branch Overview

{{< cards >}}
  {{< card link="#gimp-source" title="gimp-source" subtitle="GIMP master clone with CI and submodule adaptations" >}}
  {{< card link="#convert-tool-preset" title="convert-tool-preset" subtitle="Utility branch with data structures needed by other branches" >}}
  {{< card link="#convert-icon-picker" title="convert-icon-picker" subtitle="Icon picker interface enhancements" >}}
  {{< card link="#convert-pref-all-merged" title="convert-pref-all-merged" subtitle="Preferences system modifications" >}}
{{< /cards >}}

---

<div class="feature-section" id="gimp-source">

## gimp-source

**Purpose**: Clone of GIMP master with CI configuration adapted for Artbox development.

**Role**: Starting point for all Artbox development, providing a clean GIMP base with Artbox-specific modifications.

**Files Modified**:
- `.gitlab-ci.yml` → `.gitlab-ci-master.yml` (CI configuration backup)
- `.gitmodules` (submodule reference updates)
- `gimp-data` (submodule pointer updates)

**Implementation**: Clones GIMP master and makes infrastructure changes. The GitLab CI configuration is backed up and modified for Artbox's build pipeline, git submodule references are updated to point to Artbox-compatible versions, and the gimp-data submodule is adjusted.

</div>

<div class="feature-section" id="convert-tool-preset">

## convert-tool-preset

**Purpose**: Utility branch providing data structures for tool presets that other convert branches depend on.

**Role**: Foundation branch that must be processed first in any construction sequence, providing core tool preset functionality.

**Files Modified**:
- `app/core/gimptoolpreset.c` (280 lines added/modified - core tool preset implementation)
- `app/core/gimptoolpreset.h` (15 lines modified - tool preset interface)
- `app/widgets/gimpdeviceinfo.c` (8 lines modified - device integration)
- `app/widgets/gimptoolpreseteditor.c` (44 lines modified - preset editor improvements)

**Implementation**: Expands tool preset functionality with 275 net lines of new code. The core changes in `gimptoolpreset.c` provide data structures and handling for tool presets, while header modifications in `gimptoolpreset.h` expose new interfaces. Device integration improvements in `gimpdeviceinfo.c` ensure interaction with input devices, and the preset editor receives enhanced functionality. These modifications form the foundation that other convert branches rely on for tool management.

</div>

<div class="feature-section" id="convert-icon-picker">

## convert-icon-picker

**Purpose**: Icon picker interface enhancements.

**Role**: Improved icon selection and management.

**Files Modified**:
- `app/widgets/gimpdynamicseditor.c`
- `app/widgets/gimpiconpicker.c`
- `app/widgets/gimpiconpicker.h`
- `app/widgets/gimppropwidgets.c`
- `app/widgets/gimppropwidgets.h`
- `app/widgets/gimptemplateeditor.c`
- `app/widgets/gimptoolpreseteditor.c`

**Implementation**: Enhances the icon picker interface for better icon selection and visual feedback.

</div>

<div class="feature-section" id="convert-pref-all-merged">

## convert-pref-all-merged

**Purpose**: Preferences system overhaul introducing selection highlighting, path visualization, and configuration management for Artbox-specific features.

**Role**: Configuration system expansion that provides the foundation for user customization and visual feedback systems throughout Artbox.

**Files Modified** (10 files, 1343 insertions, 19 deletions):
- `app/config/gimpcoreconfig.c` (93 insertions, 1 deletion): Core configuration with selection highlighting and path line properties
- `app/config/gimpcoreconfig.h` (6 insertions): New configuration property declarations
- `app/config/gimpdisplayconfig.c` (14 insertions): Display-specific configuration enhancements
- `app/config/gimpdisplayconfig.h` (1 insertion): Display configuration property declarations
- `app/config/gimpguiconfig.c` (566 insertions, 1 deletion): Major GUI configuration expansion with advanced user interface options
- `app/config/gimpguiconfig.h` (38 insertions): Extensive GUI configuration property declarations
- `app/config/gimprc-blurbs.h` (29 insertions): Configuration help text and descriptions
- `app/dialogs/preferences-dialog-utils.c` (298 insertions): New preference dialog utility functions
- `app/dialogs/preferences-dialog-utils.h` (8 insertions): Preference dialog utility declarations
- `app/dialogs/preferences-dialog.c` (309 insertions, 1 deletion): Major preferences dialog expansion

**Implementation**: This branch represents an enhancement to Artbox's configuration system with several improvements:

1. **Selection Highlighting System**: Introduces selection visualization options:
   - `PROP_SELECTION_HIGHLIGHTING`: Boolean toggle for selection highlighting feature
   - `PROP_SELECTION_HIGHLIGHT_COLOR`: Customizable selection highlighting color (default: black with 0.5 alpha)
   - `PROP_SELECTION_LINE_WIDTH`: Configurable selection line thickness
   - `PROP_SELECTION_LINE_ALPHA`: Adjustable selection line transparency

2. **Path Visualization**: Adds path rendering controls:
   - `PROP_PATH_LINE_WIDTH`: Customizable path line thickness for better visibility
   - `PROP_PATH_LINE_ALPHA`: Adjustable path line transparency for optimal contrast

3. **GUI Configuration Expansion**: Enhancement to GUI configuration (566 lines added) including:
   - User interface customization options
   - Layout and behavior controls
   - Accessibility features
   - Workflow optimization settings

4. **Preference Dialog System Overhaul**: Expansion of preference management:
   - New utility functions (298 lines) for preference dialog construction
   - Preference organization and categorization
   - Improved user experience for configuration management
   - Better validation and error handling

5. **Configuration Architecture Enhancement**: Improved configuration system architecture with:
   - Better property management and type safety
   - Default value handling
   - Improved configuration persistence
   - Better integration with Artbox-specific features

This overhaul provides users with customization capabilities while establishing a foundation for Artbox's visual feedback and user interface systems.

</div>