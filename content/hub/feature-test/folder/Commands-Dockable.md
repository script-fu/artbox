---
type: docs
url: "hub/feature-test/folder/Commands-Dockable"
---

# Commands Dockable

Visual grid interface for custom commands and plugins, providing a clickable macro palette that replaces complex keyboard shortcuts.

[YouTube demonstration video.](https://youtu.be/gzhXuNBbSFM)

## Key Concepts and Definitions

- **Commands Dockable**: A dockable dialog for managing custom commands and plugins
- **Command Editor**: Editor for creating and modifying command items
- **Command Item**: A stored command with metadata including name, description, icon, and language
- **Visual Grid**: Grid view mode displaying commands as clickable icons for easy access

## Core Features

{{< cards >}}
  {{< card link="#visual-grid-interface" title="Visual Grid Interface" subtitle="Clickable macro palette replacing keyboard shortcuts with visual command grid." icon="view-grid" >}}
  {{< card link="#command-management" title="Command Management" subtitle="Create, duplicate, save, execute, and delete custom commands." icon="terminal" >}}
  {{< card link="#visual-editor" title="Visual Editor" subtitle="Editor interface with text input and metadata management." icon="code" >}}
  {{< card link="#file-format-support" title="File Format Support" subtitle="Standard .gcmd file format with serialization support." icon="save" >}}
{{< /cards >}}

---

<div class="feature-section" id="visual-grid-interface">

## Visual Grid Interface

**Current Design**: **New Feature**

**Implementation**: Grid view mode displaying commands as clickable icons, providing a visual macro palette for rapid access to frequently used operations.

**Key Benefits**:

- **Visual Access**: Commands displayed as labeled icons in grid layout
- **Plugin Integration**: Can execute any GIMP plugin or procedure through PDB calls
- **Macro Palette**: Replace complex keyboard shortcuts with single clicks
- **Custom Workflows**: Build personalized toolsets for specific tasks
- **Quick Execution**: One-click access to frequently used commands and plugins

**Use Cases**: Create visual palettes for layer operations, filter sequences, export macros, custom brush setups, or any repetitive workflow that would normally require multiple menu navigations or keyboard shortcuts.

</div>

---

<div class="feature-section" id="command-management">

## Command Management

**Current Design**: **New Feature**

**Implementation**: Command lifecycle management through a dockable dialog. Commands are stored as `GimpCommandItem` objects with properties for name, command code, description, icon, and language.

**Core Operations**:

- **New Command**: Create empty command items
- **Duplicate Command**: Clone existing commands
- **Save Command**: Persist commands to `.gcmd` files
- **Execute Command**: Run commands through appropriate interpreter
- **Delete Command**: Remove commands with confirmation

</div>

---

<div class="feature-section" id="visual-editor">

## Visual Editor

**Current Design**: **New Feature**

**Implementation**: `GimpCommandEditor` widget for command creation and modification.

**Editor Components**:

- **Name Entry**: Command identification and display name
- **Command Text View**: Multi-line text input widget for script content
- **Description Entry**: Documentation and usage notes
- **Icon Picker**: Icon selection from available GIMP icon set with custom image assignment capability
- **Language Property**: Language setting (script-fu or python)

</div>

---

---

<div class="feature-section" id="file-format-support">

## File Format Support

**Current Design**: **New Feature**

**Implementation**: `.gcmd` (GIMP Command) file format with GimpConfig serialization.

**File Format Structure**:

```text
# GIMP command item
(name "Command Name")
(command "script content")
(description "Command description")
(icon-name "icon-identifier")
(language script-fu|python)
# end of GIMP command item
```

**Storage**:

- **User Directory**: Commands stored in `~/.config/GIMP/commands/`
- **System Commands**: Pre-installed examples in application data directory
- **Auto-loading**: Commands loaded on GIMP startup

</div>

---

<div class="feature-section" id="factory-integration">

## Factory Integration

**Current Design**: **New Feature**

**Implementation**: Integration with GIMP's data factory system through `GimpCommandFactory`.

**Features**:

- **Resource Loading**: Discovery and loading of `.gcmd` files
- **Factory View**: Visual command browser with hover states
- **Container Integration**: Commands appear in standard GIMP resource containers
- **Menu Integration**: Accessible through Windows > Dockable Dialogs menu

</div>
