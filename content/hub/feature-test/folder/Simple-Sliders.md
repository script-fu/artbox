---
type: docs
---

# Objective

Simplify the slider interaction and provide a less distracting slider cursor.

## Design Revisions

| **Revision**  | **Current Design**  | **Issues**  | **Proposed Changes** |
|---------------|---------------------|-------------|----------------------|
| **1. Click to Slide** | Clicking the numerical area of the slider does not move the slider. | Adjusting values at the top range requires careful cursor control to avoid accidentally activating the numerical input. | Remove detection of left clicking in the numerical input area. |
| **2. Click to Enter Number** | Clicking the numerical area of activates the number entry. | This disrupts slider use. | Clicking the slider activates the numerical entry and allows the slider to slide  |
| **3. Grab icons changed** | Grabbing hand icons are used | This is obscuring and cartoon like | Use sb_up_arrow and sb_h_double_arrow, up and side-to-side. |

## MR Description

This MR improving slider usability for painters, interaction is simple.
It also changes the cursors from grabbing hands to sb_up_arrow and sb_h_double_arrow, up and side-to-side.

### Benefit

- Sliders will always slide on a single click, improving usability during tasks like painting.

### Loss

- Left clicking the numerical input entry will cause the slider to jump to that position and the value will change.
- User has to adapt by right clicking the numerical input for a number change without slider and value jump.
