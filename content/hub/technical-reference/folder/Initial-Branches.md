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
