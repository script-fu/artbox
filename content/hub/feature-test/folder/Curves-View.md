---
type: docs
url: "hub/feature-test/folder/Curves-View"
---

# Objective

Enhance the Curve View in the Dynamics Editor and Curves Filter.

## Design Revisions

{{< cards >}}
  {{< card link="#grid-line-visibility" title="Grid Line Visibility" subtitle="Consistent visibility across backgrounds" icon="view-grid" >}}
  {{< card link="#coordinate-display-refinement" title="Coordinate Display Refinement" subtitle="Improved X,Y coordinate display" icon="map" >}}
  {{< card link="#curve-point-visibility" title="Curve Point Visibility" subtitle="Enhanced visibility for 4K displays" icon="eye" >}}
  {{< card link="#shift-key-curve-movement" title="Shift-Key Curve Movement" subtitle="Move all curve points together" icon="arrows-expand" >}}
{{< /cards >}}

---

<div class="feature-section" id="grid-line-visibility">

## Grid Line Visibility

**Current State**: See the Curves Filter or Dynamics Curve graphs.

**Issue**: Grid lines in the Curve View are not consistently visible across different background tones.

**Solution**: Added rendering modes to grid lines, ensuring consistent visibility regardless of the background tone.

**Implementation**: Implemented rendering modes for grid lines, ensuring consistent visibility across various background tones in the Curve View.

**Benefits**: Enhanced usability through consistent grid line visibility makes the Curve View easier to interpret and use across different visual contexts.

</div>

<div class="feature-section" id="coordinate-display-refinement">

## Coordinate Display Refinement

**Current State**: X, Y coordinate display in the Curve View.

**Issue**: The current X, Y coordinate display uses block highlighting, which is visually obtrusive.

**Solution**: Refined the X, Y coordinate display to avoid block highlighting, improving user experience.

**Implementation**: Redesigned the X, Y coordinate display to eliminate block highlighting, improving readability and reducing visual distraction.

**Benefits**: Refined coordinate displays improve visual clarity and reduce interface clutter, making the Curve View more intuitive to use.

</div>

<div class="feature-section" id="curve-point-visibility">

## Curve Point Visibility

**Current State**: Curve points in the Curve View.

**Issue**: Curve points are difficult to see and select, especially on high-resolution displays (e.g., 4K).

**Solution**: Enhanced curve point visibility and selection, optimizing for 4K displays and ensuring ease of use.

**Implementation**: Enhanced the visibility and selection of curve points, particularly on high-resolution (e.g., 4K) displays, for a more accessible user experience.

**Benefits**: Optimized for high resolution displays, ensuring seamless usability on 4K displays and beyond with improved curve point visibility.

</div>

<div class="feature-section" id="shift-key-curve-movement">

## Shift-Key Curve Movement

**Current State**: Curve manipulation in the Curve View.

**Issue**: No mechanism exists to move all curve points simultaneously, limiting flexibility in curve adjustments.

**Solution**: Added a new feature: holding the Shift key allows all curve points to move together, enabling global curve adjustments.

**Implementation**: Introduced the ability to move all curve points simultaneously by holding down the Shift key, providing a quick and efficient way to adjust the entire curve.

**Benefits**: Increased flexibility through simultaneous movement of all curve points enables efficient global adjustments and streamlined workflows for complex curve editing.

</div>


