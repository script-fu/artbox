---
type: docs
---

# Objective

The brush aspect ratio should be easily understood, and predictable to use. A fine line should be achievable by creating a _very_ squashed circle.

## Design Revisions

| **Revision**  | **Current Design**  | **Issues**  | **Changes** |
|--------------------------------------------|---------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------|-----------------------------------------------------------|
| **1. Use Normalized Aspect ratio** | Range is from -20 to 20, 0 is undistorted, non-linear distortion up to 20 where there is a distortion clamp that limits the effect. | Historical reasons that are confusing in the GUI and confusing in the code | An aspect ratio of 1 is undistorted, 0, is very distorted, -1 flips the brush stamp, linear distortion |

### Changes

1. **Normalized Aspect Ratio**:
   - Replaced the old non-linear aspect ratio range of `-20 to 20` with a simplified linear range from `-1 to 1`, where `1` means undistorted, `0` represents high distortion, and `-1` flips the brush stamp.
   - The aspect ratio is now applied directly, and non-linear clamping behavior is removed.
   - Special handling for `0` aspect ratio is introduced to prevent problematic behavior, ensuring a minimal distortion of `0.005` when set to `0`.

2. **Code Adjustments for Consistency**:
   - Updated the aspect ratio scaling logic in the `gimp_brush_transform_get_scale`, `gimp_brush_generated_transform_size`, and related functions to reflect the linear aspect ratio system.
   - Refactored the calculation logic to remove historical non-linear clamps and simplify the math, providing a clearer, more predictable transformation.

3. **UI Simplifications**:
   - The brush editor now uses a `-1 to 1` range for the aspect ratio, with linear steps for finer control.
   - Updated the PDB interface to reflect the new range, removing the old `-20 to 20` bounds for both internal and user-accessible API calls.

### **Benefits**

- These changes simplify the brush aspect ratio behavior, making the interface easier to understand for users. The predictable linear distortion improves usability and allows finer control over the brush appearance. Additionally, the internal code is now cleaner and more maintainable, reducing complexity while ensuring consistent behavior across all brush-related features.
