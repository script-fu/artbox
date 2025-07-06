---
type: docs
url: "hub/feature-test/folder/Resource-Control"
---

# Resource Control

Improve the usability and data saving of resources and Tool Presets in Artbox.

{{< cards >}}
  {{< card link="#deactivate-automatic-saving" title="Deactivate Automatic Saving" subtitle="Control when resources are saved" icon="cog" >}}
  {{< card link="#immediate-saving" title="Immediate Saving" subtitle="Save specific changes immediately" icon="save" >}}
  {{< card link="#save-as-functionality" title="Save As Functionality" subtitle="Custom naming for resources" icon="save-as" >}}
  {{< card link="#save-all-changes" title="Save All Changes" subtitle="Batch save all active tool assets" icon="archive" >}}
  {{< card link="#simpler-menus" title="Simpler Menus" subtitle="Hide rarely used menu items" icon="menu" >}}
  {{< card link="#brush-editor-enhancements" title="Brush Editor Enhancements" subtitle="Improved brush type handling" icon="pencil" >}}
  {{< card link="#locked-resource-notification" title="Locked Resource Notification" subtitle="Clear feedback for locked resources" icon="lock-closed" >}}
  {{< card link="#copy-paste-new-brush" title="Copy and Paste as New Brush" subtitle="Create brushes from drawables" icon="duplicate" >}}
  {{< card link="#tool-preset-name-display" title="Tool Preset Name Display" subtitle="Show active preset in title" icon="tag" >}}
  {{< card link="#preferences-folder-options" title="Preferences Folder Options" subtitle="Manage resource folder paths" icon="folder" >}}
  {{< card link="#resource-filtering" title="Resource Filtering" subtitle="Optional filtering and tagging" icon="filter" >}}
  {{< card link="#icon-view-preview" title="Icon View Preview" subtitle="Simplified theme background" icon="photograph" >}}
{{< /cards >}}

---

<div class="feature-section" id="deactivate-automatic-saving" tabindex="-1">

## Deactivate Automatic Saving

**Current Design**: Saves are done when GIMP exits

**Issues**: Tweaks to resources in session can corrupt carefully set up tools with unwanted changes.

**Changes**: A Preference to 'Save resource changes on exit'

**Implementation**: Added a user preference option to control when resource changes are saved, preventing automatic saving of temporary modifications that might compromise carefully configured tool setups.

**Benefits**: Provides better control over resource preservation, allowing users to experiment with resource changes without fear of corrupting their carefully configured tools and presets.

</div>

<div class="feature-section" id="immediate-saving" tabindex="-1">

## Immediate Saving

**Current Design**: Saves are done when GIMP exits

**Issues**: Changes to resources are lost if GIMP crashes or exits with a crash.

**Changes**: Save immediately when clicked

</div>

<div class="feature-section" id="save-as-functionality" tabindex="-1">

## Save As Functionality

**Current Design**: Saves are done with default naming

**Issues**: The name of the saved resource is not the same as the filename, this is confusing.

**Changes**: Save immediately with a naming option, Save As...

</div>

<div class="feature-section" id="save-all-changes" tabindex="-1">

## Save All Changes

**Current Design**: If saves are done by the user on demand, as described in (2) or (3), a new issue arises

**Issues**: Changes to resources may be forgotten during the session. Saving one by one is error prone and time consuming

**Changes**: Add 'Save all the active tool assets' button and a 'Save all changes' button on the Preset Editor

</div>

<div class="feature-section" id="simpler-menus" tabindex="-1">

## Simpler Menus

**Current Design**: Menu item 'Copy Resource Location' exists in several menus

**Issues**: Not used by most users, creates menu clutter

**Changes**: A Preference to 'Show Copy Resource Location menu item'

</div>

<div class="feature-section" id="brush-editor-enhancements" tabindex="-1">

## Brush Editor Enhancements

**Current Design**: See menu items and Button Bar GUI in GIMP / See Brushes Menu items

**Issues**: Confusing item placement, Button Bar GUI out of step with updates / Confusion over brush types

**Changes**: Apply a consistent menu item position, and arrange Button Bars to support the changes / Double clicking an image type opens the image for editing, Double clicking a parametric type opens the Brush Editor

</div>

<div class="feature-section" id="locked-resource-notification" tabindex="-1">

## Locked Resource Notification

**Current Design**: Folder locked resources can not be edited

**Issues**: User confusion

**Changes**: An informative message is displayed in the Brush Editor if the resource is locked

</div>

<div class="feature-section" id="copy-paste-new-brush" tabindex="-1">

## Copy and Paste as New Brush

**Current Design**: New Feature

**Issues**: Create a brush from the active drawable

**Changes**: Added to the Brushes Menu via a Script-Fu plug-in

</div>

<div class="feature-section" id="tool-preset-name-display" tabindex="-1">

## Tool Preset Name Display

**Current Design**: New Feature

**Issues**: See the active Tool Preset name requires the Tool Preset Editor to be open or the Tool Preset selector to be in list mode

**Changes**: Added the active Tool Preset name after the Tool name in the Tool Options title. Tool Name | Tool Preset Name

</div>

<div class="feature-section" id="preferences-folder-options" tabindex="-1">

## Preferences Folder Options

**Current Design**: New Feature

**Issues**: Folders have to be manually added or removed per resource

**Changes**: Added a GUI to add, deactivate, or remove folder paths to a set of resources, allowing quick control over active resources

</div>

<div class="feature-section" id="resource-filtering" tabindex="-1">

## Resource Filtering

**Current Design**: New Feature

**Issues**: User never uses filtering and it takes up GUI space and adds complexity

**Changes**: Added Preference option, Interface > Resource Filtering > Enable Resource Filtering and Tagging

</div>

<div class="feature-section" id="icon-view-preview" tabindex="-1">

## Icon View Preview

**Current Design**: Themes button appears in Icon view grid modes to toggle background colour of preview

**Issues**: Adds GUI clutter that also appears in the Tool Presets view, user sets once, button hangs around forever.

**Changes**: Hardcode the previews to use the theme background colour and hide the toggle button.

**Implementation**: Automatically configured icon view previews to use theme background colors and removed the persistent toggle button, eliminating interface clutter while maintaining visual consistency.

**Benefits**: Reduces GUI complexity by removing a rarely-used persistent button, while maintaining appropriate theme-based preview backgrounds for better visual integration.

</div>

---

## Development Challenges

**Architectural Complexity**

Resource Control represents one of the most comprehensive feature implementations in Artbox due to GIMP's unified resource architecture. The feature required modifications across 74 files with over 5,000 lines of changes, touching every layer of the application from core data management to user interface elements.

**Interconnected Systems**

GIMP's resource system (brushes, gradients, patterns, palettes, tool presets) shares unified factories, data models, action handlers, and UI widgets. Modifying saving behavior for one resource type necessitates coordinated updates across all resource types to maintain consistency. This architectural reality makes isolated changes impossible.

**Cross-Cutting Implementation**

The feature spans multiple subsystems simultaneously:
- Core data factories and object models
- Action system commands and handlers
- Widget hierarchy and editor components
- Menu system integration and sensitivity
- Preferences storage and management
- Build system configuration

**Why Monolithic Approach Was Required**

Alternative implementation strategies proved unworkable:
- **Gradual Implementation**: Would leave the system in broken intermediate states
- **Feature Flags**: Would require maintaining dual code paths permanently throughout the codebase
- **Modular Separation**: Impossible due to circular dependencies and compilation requirements

**API Breaking Changes**

Core function signatures required modification to support custom naming functionality. These changes propagated through the entire codebase, forcing synchronized updates across all resource-handling components to maintain API consistency.

**Build-Time Feature Control**

To manage this complexity, Resource Control can be included or excluded at build time through construction scripts, providing deployment flexibility while maintaining code integrity.


