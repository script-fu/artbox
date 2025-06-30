---
type: docs
url: "hub/feature-test/folder/Simple-Sliders"
---

# Simple Sliders

Simplify the slider interaction and provide a less distracting slider cursor.

{{< cards >}}
  {{< card link="#click-to-slide" title="Click to Slide" icon="hand" >}}
  {{< card link="#click-to-enter-number" title="Click to Enter Number" icon="calculator" >}}
  {{< card link="#grab-icons-changed" title="Grab Icons Changed" icon="cursor-click" >}}
  {{< card link="#ctrl-clicking" title="Ctrl Clicking" icon="terminal" >}}
  {{< card link="#optional-reset-and-link-buttons" title="Optional Reset and Link Buttons" icon="cog" >}}
{{< /cards >}}

---

<div class="feature-section" id="click-to-slide" tabindex="-1">

## Click to Slide

**Current Design:** Clicking the numerical area of the slider does not move the slider.

**Issues:** Adjusting values at the top range requires careful cursor control to avoid accidentally activating the numerical input.

**Changes:** Remove detection of left clicking in the numerical input area.

**Implementation:** Modified slider behavior to allow single-click sliding across the entire slider area, including the numerical display area, eliminating the need for precise cursor positioning.

**Benefits:** Sliders will always slide on a single click, significantly improving usability during painting tasks by reducing the precision required for slider interaction.

</div>

<div class="feature-section" id="click-to-enter-number" tabindex="-1">

## Click to Enter Number

**Current Design:** Clicking the numerical area activates the number entry.

**Issues:** This disrupts slider use.

**Changes:** Clicking the slider activates the numerical entry and allows the slider to slide.

**Implementation:** Unified slider and numerical entry activation, allowing both sliding and number input activation from the same click area for improved workflow integration.

**Benefits:** Provides flexible input methods without interface disruption, enabling smooth transitions between sliding and precise numerical input.

</div>

<div class="feature-section" id="grab-icons-changed" tabindex="-1">

## Grab Icons Changed

**Current Design:** Grabbing hand icons are used.

**Issues:** This is obscuring and cartoon like.

**Changes:** Use sb_up_arrow and sb_h_double_arrow, up and side-to-side.

**Implementation:** Replaced cartoon-style grabbing hand icons with clean, professional directional arrow cursors (sb_up_arrow and sb_h_double_arrow) that provide clear directional feedback without visual obstruction.

**Benefits:** Eliminates cartoon-like visual elements and provides clearer, less distracting cursor feedback that doesn't obscure the slider values during interaction.

</div>

<div class="feature-section" id="ctrl-clicking" tabindex="-1">

## Ctrl Clicking

**Current Design:** New Feature.

**Issues:** Reset Button is **optionally** hidden.

**Changes:** `Ctrl Left Click` the slider to reset it.

**Implementation:** Added keyboard shortcut functionality allowing Ctrl+Left Click on any slider to instantly reset it to default values, providing an alternative to reset buttons.

**Benefits:** Enables quick slider resets even when reset buttons are hidden, maintaining functionality while supporting simplified GUI preferences.

</div>

<div class="feature-section" id="optional-reset-and-link-buttons" tabindex="-1">

## Optional Reset and Link Buttons

**Current Design:** Reset and Brush Link buttons are always displayed.

**Issues:** Buttons are **optionally** hidden.

**Changes:** Preferences > Tool Options > Paintbrush Tool > Show Brush Reset Buttons & Show Brush Update Buttons.

**Implementation:** Added preference controls in Tool Options > Paintbrush Tool to selectively show or hide Reset and Brush Update buttons, allowing users to customize their interface complexity.

**Benefits:** Users can simplify the GUI by hiding unwanted buttons through preference options, creating a cleaner, more personalized workspace that reduces visual clutter during painting tasks.

</div>


