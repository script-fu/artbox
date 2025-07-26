---
type: docs
url: "hub/feature-test/folder/Commands-Dockable"
---

# Commands Dockable

Command management and automation system for Artbox that supports manual execution and event-driven automation with signal coalescing and asynchronous execution.

[YouTube demonstration video.](https://youtu.be/gzhXuNBbSFM)

## Key Concepts

- **Commands Dockable**: A dockable dialog for managing custom commands with manual and event-driven execution
- **Command Editor**: Interface for creating and editing commands with event trigger configuration and signal coalescing controls
- **Command Item**: A stored command with name, description, icon, language, and optional event trigger with coalescing properties
- **Event-Driven Automation**: Commands that automatically execute when Artbox events occur with signal storm protection
- **Signal Monitoring**: System for connecting commands to 14 Artbox signals including layer changes, tool selection, and image modifications
- **Signal Coalescing**: Per-command configurable thresholds (1-5000ms) prevent signal storms while maintaining responsiveness

## Core Features

{{< cards >}}
  {{< card link="#command-management" title="Command Management" subtitle="Create, edit, save, execute, and delete custom commands with full lifecycle management." icon="terminal" >}}
  {{< card link="#event-automation" title="Event Automation" subtitle="Commands respond to Artbox signals automatically with signal coalescing protection." icon="lightning-bolt" >}}
  {{< card link="#dual-language-support" title="Dual-Language Support" subtitle="Script-Fu and Python command execution with asynchronous processing." icon="code" >}}
  {{< card link="#signal-monitoring" title="Signal Monitoring" subtitle="Monitor 14 Artbox signals with per-command configurable coalescing thresholds." icon="chart-square-bar" >}}
  {{< card link="#command-editor" title="Command Editor" subtitle="Visual editor with event trigger configuration and coalescing controls." icon="pencil" >}}
  {{< card link="#file-format" title="File Format" subtitle="Extended .gcmd file format with event and coalescing properties." icon="save" >}}
{{< /cards >}}

---

## Command Management

Commands are stored as objects with properties for manual execution and event automation. The dockable provides standard operations:

- **New Command**: Create empty command items
- **Duplicate Command**: Clone existing commands
- **Save/Load**: Persist commands to `.gcmd` files
- **Execute Command**: Run commands with appropriate interpreter
- **Delete Command**: Remove commands with confirmation

The interface supports double-click execution, context menus, and standard Artbox selection behaviors.

---

## Event Automation

Commands can be configured to execute automatically when Artbox events occur. The system monitors events with signal coalescing to prevent performance issues:

**Available Signals** (14 total):

- **Image Events** (3): dirty, image-changed, add
- **Layer Events** (5): layer-added, opacity-changed, mode-changed, visibility-changed, layer-selected  
- **Layer Mask Events** (4): edit-mask-changed, apply-mask-changed, show-mask-changed, layer-mask-selected
- **Tool Events** (2): tool-changed, brush-changed

**Signal Coalescing**:

- **Per-command thresholds**: Configurable from 1-5000ms (default 100ms)
- **Signal storm protection**: Rejects duplicate signals within threshold window
- **Performance benefits**: Up to 84.6% signal reduction during stress testing
- **Queue management**: Handles up to 107+ pending signals with depth tracking

**Execution Patterns**:

- **Execute-Once**: Commands run once then disconnect automatically with race condition protection
- **Continuous**: Commands remain connected for ongoing monitoring with coalescing
- **Asynchronous Execution**: All commands use `g_idle_add_full()` for non-blocking execution

---

## Dual-Language Support

The system supports both Script-Fu and Python commands with asynchronous execution:

- **Script-Fu**: Uses `plug-in-script-fu-eval` for execution with GLib idle mechanism
- **Python**: Uses `python-fu-eval` for execution with GLib idle mechanism
- **Language Detection**: Commands routed to appropriate interpreter based on language property
- **Asynchronous Processing**: Commands execute in background without blocking UI or system
- **Error Handling**: Comprehensive error reporting with language-specific context

---

## Signal Monitoring

The system provides comprehensive signal monitoring with intelligent filtering and performance protection:

**Signal Categories**:

- **Image Category**: Image state and lifecycle events (3 signals)
- **Layer Category**: Layer management and property changes (5 signals including granular layer selection)
- **Layer Mask Category**: Layer mask management and editing (4 signals)
- **Tool Category**: Tool selection and configuration changes (2 signals)

**Signal Intelligence**:

- **Selection Filtering**: Layer-specific signals only emit for currently selected layers
- **Centralized Logic**: Signal emission intelligence concentrated in Artboximage.c
- **Manual Forwarding**: Core layer functions call notification functions which conditionally emit signals
- **Minimal Core Changes**: Well-tested core code preserved with only essential notification additions

**Performance Monitoring**:

- **Real-time Statistics**: Signal processing metrics with coalescing effectiveness tracking
- **Queue Depth Tracking**: Real-time monitoring of pending signal counts
- **Sequence Numbering**: Global sequence tracking for signal traceability
- **Debug Output**: Comprehensive logging for signal flow analysis

---

## Command Editor

The editor provides controls for both manual and event-driven commands with advanced coalescing configuration:

**Basic Properties**:

- Name, command text, description, icon selection
- Language setting (Script-Fu or Python)
- Enabled state control for command activation

**Event Configuration**:

- Signal selection dropdown organized by category (Image, Layer, Layer Mask, Tool)
- Execute-once checkbox for one-time automation with race condition protection
- Real-time validation of signal assignments with feedback

**Signal Coalescing Controls**:

- "Execute every signal" checkbox with inverted logic (checked = no coalescing)
- Threshold spinbox for coalescing threshold (1-5000ms) shown when coalescing enabled
- Safety warning when coalescing disabled: "⚠️ Warning: Commands may trigger themselves, other commands, or be triggered by automation scripts. This creates complex interactions - use with caution."

**File Creation**: Creates complete .gcmd files when signals are selected with all properties

---

## File Format

Commands use the `.gcmd` format with optional event and coalescing properties:

```text
# Artbox command item
(name "Auto-Save Monitor")
(command "(Artbox-file-save ...)")
(description "Automatically saves image when dirty")
(icon-name "Artbox-marker")
(language script-fu)
(event-signal "dirty")
(enabled yes)
(execute-once no)
(coalesce-signals yes)
(coalesce-threshold-ms 100)
# end of Artbox command item
```

**Format Features**:

- **Backward Compatibility**: Existing commands work without coalescing properties
- **Event Properties**: Event-driven and coalescing properties optional with sensible defaults
- **Language Specification**: Language declaration for Script-Fu or Python
- **Execute-Once Control**: Boolean flag for one-time execution behavior
- **Coalescing Control**: Boolean flag and threshold for signal storm protection
- **Property Validation**: Signal validation during load with error reporting

**Storage**:

- User commands: `~/.config/Artbox/commands/` with automatic directory creation
- System commands: Application data directory with pre-installed examples
- Auto-loading on Artbox startup with path resolution
- Path configuration through Artbox preferences
