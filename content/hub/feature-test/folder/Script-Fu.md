---
type: docs
url: "hub/feature-test/folder/Script-Fu"
---

# Script-Fu

Extend Script-Fu to include additional functions that help the user.

## Key Concepts and Definitions

- **Script-Fu**: A scripting language based on Scheme

## Additional Procedures

{{< cards >}}
  {{< card link="#display-functions" title="Display Functions" subtitle="Get active display ID for display-related operations." icon="desktop-computer" >}}
  {{< card link="#eraser-toggle-functions" title="Eraser Toggle Functions" subtitle="Toggle between eraser and other painting tools." icon="pencil" >}}
  {{< card link="#visibility-functions" title="Visibility Functions" subtitle="Manage visibility of multiple items in bulk." icon="eye" >}}
  {{< card link="#brush-control-functions" title="Brush Control Functions" subtitle="Control brush scale and jitter settings." icon="terminal" >}}
  {{< card link="#layer-functions" title="Layer Functions" subtitle="Combine alpha channels and transfer content between layers." icon="duplicate" >}}
{{< /cards >}}

---

<div class="feature-section" id="display-functions">

## Display Functions

| **Command** | **Purpose** |
| --- | --- |
| `(gimp-context-get-display)` | Get the active display ID |

**Implementation**: This function retrieves the active display ID which can be used with other display-related functions like `(gimp-display-present display-id)` for script automation and display management.

</div>

---

<div class="feature-section" id="eraser-toggle-functions">

## Eraser Toggle Functions

| **Command** | **Purpose** |
| --- | --- |
| `(gimp-context-eraser-toggle)` | Toggle the active tool to the eraser |
| `(gimp-context-eraser-paintbrush-toggle)` | Toggle the active tool to the eraser and always return to the paintbrush |
| `(gimp-context-get-eraser-active)` | Returns true if the Eraser Tool is active |

**Implementation**: These functions enable seamless tool switching, allowing scripts to toggle between the eraser and other painting tools. The paintbrush toggle ensures consistent tool return behavior for predictable workflows.

</div>

---

<div class="feature-section" id="visibility-functions">

## Visibility Functions

| **Command** | **Purpose** |
| --- | --- |
| `(gimp-items-set-visible)` | Set the visibility of a vector list of items |

**Implementation**: Allows setting the visibility of a vector list of items in bulk, streamlining visibility management for layers, paths, or other drawable items in complex compositions with many elements.

</div>

---

<div class="feature-section" id="brush-control-functions">

## Brush Control Functions

| **Command** | **Purpose** |
| --- | --- |
| `(gimp-context-get-brush-eraser-scale)` | Returns the Paint Tool eraser scale |
| `(gimp-context-get-brush-jitter)` | Returns the Paint Tool jitter slider value |
| `(gimp-context-set-brush-jitter)` | Set _all_ the Paint Tools jitter slider values |

**Implementation**:

- **Eraser Scale**: Gets the Paint Tool eraser scale option for use with eraser toggles, allowing painting tool presets to have specific sized erasers. Erase pencil lines with a big eraser, cut into brush strokes with a smaller eraser.
- **Jitter Control**: Enables getting and setting jitter values across all Paint Tools (eraser, paintbrush, airbrush, pencil) for consistent brush behavior and seamless tool switching.

</div>

---

<div class="feature-section" id="layer-functions">

## Layer Functions

| **Command** | **Purpose** |
| --- | --- |
| `(gimp-layer-combine-alpha)` | Combine the alpha channels of two layers |
| `(gimp-drawable-transfer)` | Transfer content between drawable objects |

**Implementation**:

- **Alpha Combination**: The `gimp-layer-combine-alpha` procedure combines the alpha channels of two layers and writes the result into the first layer's alpha channel using operations like ADD, SUBTRACT, INTERSECT, or REPLACE for advanced compositing workflows.
- **Drawable Transfer**: The `gimp-drawable-transfer` procedure enables transferring content between drawable objects (layers, channels, layer masks) for advanced layer management and compositing operations. Importantly, it avoids any floating layer anchoring issues and automatically handles offset calculations for seamless content transfer.

</div>

---
