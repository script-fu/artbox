---
type: docs
---

# Objective

Improve the quality of the painting experience in Artbox

## Related Links

- Branches: Artbox and [feature-selection](https://gitlab.gnome.org/pixelmixer/artbox/-/tree/feature-selection?ref_type=heads)

## Design Revisions

| **Revision**  | **Current Design**  | **Issues**  | **Changes** |
|--------------------------------------------|---------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------|-----------------------------------------------------------|
| **1. Auto commit** | The selection has to be committed before another selection can be made. | It makes drawing multiple areas snaggy. | An option to `Auto commit` when a selection is made |
| **2. Fill Selection**   | New Feature | Workflow is faster and more like painting when a selection is auto filled | An option to `Fill selection` when a selection is made |
| **3. Auto Deselect**   | New Feature  | Workflow is faster, select -> fill -> see -> select -> fill | An option to `Auto deselect` when a selection is made, used after an auto fill has been done |

## MR Description (Adapted to Table Concepts)

This MR improves the painting experience by introducing new features that allow polygonal block in painting.

### Changes

1. **Auto Commit**:
   - Added a new option to automatically commit a selection once it is made, eliminating the need to manually commit before creating another selection.
   - This enhancement removes interruptions, making the process of drawing multiple areas smoother.

2. **Fill Selection**:
   - Introduced an option to automatically fill a selection once it is made.
   - This feature streamlines the workflow by simulating a painting-like experience, reducing the steps required to complete a filled selection.

3. **Auto Deselect**:
   - Added an option to automatically deselect a selection after it has been auto-filled.
   - This update enables a continuous workflow where users can effortlessly transition from selecting to filling and back to selecting again.

### Benefit

- These updates significantly enhance the usability and efficiency of the painting workflow. The `Auto Commit` feature ensures seamless transitions between selections, `Fill Selection` makes the workflow faster and more intuitive, and `Auto Deselect` reduces repetitive actions, allowing users to focus on creative tasks rather than manual steps.
