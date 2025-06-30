---
type: docs
url: "hub/feature-test/folder/Brush-Aspect-Ratio-Range"
---

# Brush Aspect Ratio Range

The brush aspect ratio should be easily understood, and predictable to use. A fine line should be achievable by creating a _very_ squashed circle.

## Design Revisions

{{< cards >}}
  {{< card link="#normalized-aspect-ratio" title="Normalized Aspect Ratio" subtitle="Linear -1 to 1 range for predictable distortion." icon="scale" >}}
{{< /cards >}}

---

<div class="feature-section" id="normalized-aspect-ratio">

## Normalized Aspect Ratio

**Current Design**: Range is from -20 to 20, 0 is undistorted, non-linear distortion up to 20 where there is a distortion clamp that limits the effect.

**Issues**: Historical reasons that are confusing in the GUI and confusing in the code.

**Changes**: An aspect ratio of 1 is undistorted, 0 is very distorted, -1 flips the brush stamp, linear distortion.

**How to Use**:

- Replaced the old non-linear aspect ratio range of `-20 to 20` with a simplified linear range from `-1 to 1`
- `1` means undistorted, `0` represents high distortion, and `-1` flips the brush stamp
- Special handling for `0` aspect ratio prevents problematic behavior, ensuring minimal distortion of `0.005`
- Updated brush editor uses `-1 to 1` range with linear steps for finer control
- PDB interface reflects the new range, removing old `-20 to 20` bounds

**Benefits**: Simplifies brush aspect ratio behavior, making the interface easier to understand. The predictable linear distortion improves usability and allows finer control over brush appearance.

</div>

---