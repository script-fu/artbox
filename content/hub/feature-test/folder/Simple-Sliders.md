---
type: docs
url: "hub/feature-test/folder/Simple-Sliders"
---

# Objective

Simplify the slider interaction and provide a less distracting slider cursor.

## Design Revisions

| **Revision**  | **Current Design**  | **Issues**  | **Proposed Changes** |
|---------------|---------------------|-------------|----------------------|
| **1. Click to Slide** | Clicking the numerical area of the slider does not move the slider. | Adjusting values at the top range requires careful cursor control to avoid accidentally activating the numerical input. | Remove detection of left clicking in the numerical input area. |
| **2. Click to Enter Number** | Clicking the numerical area of activates the number entry. | This disrupts slider use. | Clicking the slider activates the numerical entry and allows the slider to slide  |
| **3. Grab icons changed** | Grabbing hand icons are used | This is obscuring and cartoon like | Use sb_up_arrow and sb_h_double_arrow, up and side-to-side. |
| **4. Ctrl Clicking** | New Feature | Reset Button is **optionally** hidden | `Ctrl Left Click` the slider to reset it |
| **5. Optional Reset and Link Buttons** | Reset and Brush Link buttons are always displayed | Button are **optionally** hidden | Preferences > Tool Options > Paintbrush Tool > Show Brush Reset Buttons & Show Brush Update Buttons |

### **Benefits**

- Sliders will always slide on a single click, improving usability during tasks like painting.

- Users can simplify the GUI with Preference options to unwanted hide buttons.

- No cartoon hands.

- Ctrl Left clicking to reset.
