---
type: docs
---

# Objective

Simplify the slider interaction and provide a less distracting slider cursor.

## Design Revisions

| **Revision**  | **Current Design**  | **Issues**  | **Proposed Changes** |
|---------------|---------------------|-------------|----------------------|
| **1. Click to Slide** | Clicking the numerical area of the slider does not move the slider. | Adjusting values at the top range requires careful cursor control to avoid accidentally activating the numerical input. | Disable slider activation by a single click in the numerical input area. |

## MR Description

This MR removes the ability to activate the numerical input field with a single click, improving slider usability.
It also changes the cursors from grabbing hands to sb_up_arrow and sb_h_double_arrow, up and side-to-side.

### Benefit

- Sliders will always slide on a single click, improving usability during tasks like painting.
- Up arrows allow a precise selection and don't visually jump from cursor to hands, less distraction.

### Loss

- Numerical input must now be adjusted using +/-, arrow keys, page up/down, middle-click, or by double-clicking the numerical area. This change impacts quick single-click numerical edits.
