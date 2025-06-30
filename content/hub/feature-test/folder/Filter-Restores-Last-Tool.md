---
type: docs
url: "hub/feature-test/folder/Filter-Restores-Last-Tool"
---

# Filter Restores Last Tool

Removes a long-standing GUI issue.

{{< cards >}}
  {{< card link="#restore-previous-tool" title="Restore Previous Tool" subtitle="Return to last tool after filter use" icon="refresh" >}}
{{< /cards >}}

---

## Key Concepts and Definitions

- **Filter**: A plug-in that processes pixels in a drawable, Hue, Blur etc.
- **Tool Palette**: The grid of tool buttons, Move Tool, Paintbrush Tool ect.

---

<div class="feature-section" id="restore-previous-tool" tabindex="-1">

## Restore Previous Tool After Filter Use

**Current Design**: The filter is the active tool

**Issues**: Confusing to the user to deselect the active tool when a filter is used, and to keep the filter as the active tool

**Changes**: Restore the previous tool when a filter dialog is closed

**Implementation**: Added code to retrieve the previous tool from the context. After a filter dialog closes (whether committed or canceled), the previous tool is restored using `gimp_context_set_tool`.

**Benefits**: Ensures the user's previous tool is restored after using a filter, providing a more intuitive and seamless experience in the tool palette.

</div>
