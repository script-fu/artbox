---
type: docs
url: "hub/feature-test/folder/Layer-Mode-Recents"
---

# Layer Mode Recents

Provide quick access to recently used layer blend modes for faster workflow.

[YouTube demonstration video.](https://youtu.be/XG-g5TnWXFo)

## Design Revisions

{{< cards >}}
  {{< card link="#layer-mode-recents-group" title="Layer Mode Recents Group" subtitle="Dynamic recent modes list with persistence" icon="clock" >}}
{{< /cards >}}

---

<div class="feature-section" id="layer-mode-recents-group">

## Layer Mode Recents Group

**Current State**: Layer blend mode selection requires navigating through Default or Legacy mode groups to find frequently used modes.

**Issue**: Artists often use a small subset of layer modes repeatedly but have to search through the full list each time. No memory of previously used modes exists across sessions.

**Solution**: Added a new "Recent" group to the layer mode groups dropdown (the small button to the right of the layer mode selector) that maintains a dynamic list of the 5 most recently used layer modes. When a mode is selected from any other group (Default/Legacy), it automatically gets added to the top of the Recent list. The Recent group uses the Document History icon for visual consistency.

**Implementation Details**:
- Recent modes list is limited to 5 items maximum
- Selecting a mode from Recent group does not reorder the list
- Selecting from Default/Legacy groups adds the mode to Recent and moves existing matches to top
- Recent list persists between sessions in layermoderc file
- Active group selection also persists between sessions
- Smart equivalence resolution prevents unnecessary group switching when opening files

**Benefits**: Significantly reduces clicks and search time for artists who work with specific layer modes repeatedly. The persistent nature means workflow preferences are maintained across sessions. The equivalence system ensures that files using modes not in the current group still open smoothly by finding equivalent modes or falling back gracefully.

**Technical Notes**: Integrates seamlessly with existing GIMP layer mode infrastructure. Uses consolidated RC file approach following GIMP persistence patterns. Reuses existing group mapping table for mode equivalence resolution.

</div>

---
