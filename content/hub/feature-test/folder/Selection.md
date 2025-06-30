---
type: docs
url: "hub/feature-test/folder/Selection"
---

# Selection

Improve the quality of the painting experience in Artbox

{{< cards >}}
  {{< card link="#auto-commit" title="Auto Commit" subtitle="Automatically commit selections" icon="check-circle" >}}
  {{< card link="#fill-selection" title="Fill Selection" subtitle="Auto-fill selections when made" icon="color-swatch" >}}
  {{< card link="#auto-deselect" title="Auto Deselect" subtitle="Deselect after auto-fill" icon="x-circle" >}}
{{< /cards >}}

---

<div class="feature-section" id="auto-commit" tabindex="-1">

## Auto Commit

**Current Design**: The selection has to be committed before another selection can be made.

**Issues**: It makes drawing multiple areas snaggy.

**Changes**: An option to `Auto commit` when a selection is made

**Implementation**: Added an automatic selection commit option that eliminates the need for manual commitment when creating new selections, enabling seamless multi-area selection workflows.

**Benefits**: Removes workflow interruptions by automatically committing selections, making the process of drawing multiple areas smoother and more intuitive for rapid selection tasks.

</div>

<div class="feature-section" id="fill-selection" tabindex="-1">

## Fill Selection

**Current Design**: New Feature

**Issues**: Workflow is faster and more like painting when a selection is auto filled

**Changes**: An option to `Fill selection` when a selection is made

**Implementation**: Introduced an automatic selection filling option that immediately fills selections upon creation, creating a painting-like workflow experience.

**Benefits**: Streamlines the workflow by simulating a natural painting experience, reducing manual steps and enabling faster completion of filled selections for rapid artistic iteration.

</div>

<div class="feature-section" id="auto-deselect" tabindex="-1">

## Auto Deselect

**Current Design**: New Feature

**Issues**: Workflow is faster, select -> fill -> see -> select -> fill

**Changes**: An option to `Auto deselect` when a selection is made, used after an auto fill has been done

**Implementation**: Added an automatic deselection option that activates after auto-fill operations, enabling continuous select-fill-select workflows without manual deselection steps.

**Benefits**: Enables a continuous workflow where users can effortlessly transition from selecting to filling and back to selecting again, focusing on creative tasks rather than repetitive manual deselection actions.

</div>


