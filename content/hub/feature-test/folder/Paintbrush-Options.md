---
type: docs
url: "hub/feature-test/folder/Paintbrush-Options"
---

# Paintbrush Options

Improve the usability of the Paintbrush GUI and create new stroke possibilities.

## Design Revisions

{{< cards >}}
  {{< card link="#reset-brush-button" title="Reset Brush Button" subtitle="Optional reset functionality" icon="refresh" >}}
  {{< card link="#brush-link-button" title="Brush Link Button" subtitle="Optional brush editor linking" icon="link" >}}
  {{< card link="#additional-options-expander" title="Additional Options" subtitle="Collapsible lesser-used options" icon="chevron-down" >}}
  {{< card link="#separate-dynamics" title="Separate Dynamics" subtitle="Organized fade and color controls" icon="adjustments" >}}
  {{< card link="#compact-resource-chooser" title="Compact Chooser" subtitle="Streamlined resource selection" icon="selector" >}}
  {{< card link="#smooth-stroke-position" title="Smooth Stroke Position" subtitle="Better placement for frequent use" icon="cursor-click" >}}
  {{< card link="#stroke-effects-expander" title="Stroke Effects" subtitle="Organized stroke options" icon="pencil" >}}
  {{< card link="#jitter-slider" title="Jitter Slider" subtitle="Direct jitter control" icon="sparkles" >}}
  {{< card link="#eraser-slider" title="Eraser Slider" subtitle="Custom eraser sizing" icon="trash" >}}
  {{< card link="#uniform-jitter" title="Uniform Jitter" subtitle="Even jitter distribution" icon="view-grid" >}}
  {{< card link="#initial-angle" title="Initial Angle" subtitle="Brush starting angle control" icon="arrow-up" >}}
  {{< card link="#angle-blend-factor" title="Angle Blend Factor" subtitle="Interpolation control" icon="beaker" >}}
  {{< card link="#direction-stabilization" title="Direction Stabilization" subtitle="Stroke start delay" icon="clock" >}}
  {{< card link="#relative-initial-angle" title="Relative Initial Angle" subtitle="Angle offset control" icon="arrow-right" >}}
  {{< card link="#random-angle" title="Random Angle" subtitle="Controllable angle randomization" icon="sparkles" >}}
{{< /cards >}}

---

<div class="feature-section" id="reset-brush-button">

## Reset Brush Button

**Current State**: Option sliders have a reset button to default brush values.

**Issue**: Rarely used in some workflows; adds complexity to the GUI.

**Solution**: Make it optional via a Tool Options -> Paintbrush preference. Also, <kbd>Ctrl + Click</kbd> on the slider to reset it to the brush default.

**Implementation**: Made the `Reset to brush default` buttons optional. Added a new feature to <kbd>Ctrl + Right Click</kbd> to also reset the Tool Option to the brush defined setting.

</div>

<div class="feature-section" id="brush-link-button">

## Brush Link Button

**Current State**: Brush link button allows linking to brush editor options and brush changes.

**Issue**: Difficult to explain and used in some workflows, not all; causes confusion.

**Solution**: Rename the button to Brush Update Button. Make it optional via a Tool Options -> Paintbrush preference. Add more clarity and information to the tooltip.

**Implementation**: Made the 'Link to Brush Editor' button optional, which previously allowed linking the Paintbrush options to the Brush Editor options. This simplifies the GUI for those that do not use this feature.

</div>

<div class="feature-section" id="additional-options-expander">

## Additional Options Expander

**Current State**: Options are added to the end of Paintbrush settings; more options will be added in the future.

**Issue**: Lesser-used options clutter the interface and reduce dock space efficiency.

**Solution**: Add an "Additional Options" expander for lesser-used items.

**Implementation**: Introduced a new "Additional Options" expander in the Paintbrush options panel. This organizes less frequently used options (such as 'Lock Brush to View' and 'Simple Brush Boundary' toggles) into a collapsible section, saving space and reducing clutter in the GUI.

</div>

<div class="feature-section" id="separate-dynamics">

## Separate Dynamics

**Current State**: 'Enable Dynamics' contains the 'Fade and Colour' options.

**Issue**: The 'Fade and Colour' options take up a lot of space and do not need to be visible all the time.

**Solution**: Add a "Dynamic Fade and Colour" expander, visible only when Enable Dynamics is checked.

**Implementation**: Moved the 'Fade and Colour' options (related to brush dynamics) into a separate expander that appears only when 'Enable Dynamics' is checked. This keeps the interface cleaner by hiding these advanced options when dynamics are not in use. Added `fade-multiply` and `brush-pressure-multiply` toggles to enable pressure and fade dynamics, providing more fine-tuned control.

</div>

<div class="feature-section" id="compact-resource-chooser">

## Compact Resource Chooser

**Current State**: Picking a resource such as a brush or a dynamic is done via a chooser in the Paintbrush GUI.

**Issue**: The chooser takes up two rows of the dockable panel due to a label above the combo box. The icons on either side are distorted to fill the gap, which looks poor. GUI space is wasted.

**Solution**: Remove the label to make the chooser more compact. The purpose of the chooser is self-evident and does not need a label.

**Implementation**: Removed the label from the resource chooser (used for selecting brushes, dynamics, etc.), making the chooser more compact and saving space in the dockable panel. The chooser's function is self-explanatory, so the label was deemed unnecessary.

</div>

<div class="feature-section" id="smooth-stroke-position">

## Smooth Stroke Position

**Current State**: 'Smooth Stroke' is located lower down in the dock.

**Issue**: It's a frequently used option for painting.

**Solution**: Move it higher up in the dock within 'Stroke Effects'.

**Implementation**: Moved the 'Smooth Stroke' options higher up in the Paintbrush options panel, reflecting its frequent use. This improves accessibility and better aligns with user expectations.

</div>

<div class="feature-section" id="stroke-effects-expander">

## Stroke Effects Expander

**Current State**: New feature.

**Issue**: Options clutter the Paintbrush GUI, or don't flow visually.

**Solution**: Create a 'Stroke Effects' expander to organize these related options. The state of the expander is saved and restored.

**Implementation**: Added a new "Stroke Effects" expander to group related stroke options into one collapsible section. The state of the expander is saved and restored across sessions, preserving the user's preference for a consistent experience.

</div>

<div class="feature-section" id="jitter-slider">

## Jitter Slider

**Current State**: New feature.

**Issue**: Jitter was under `Apply Jitter` down the options, using relative to brush size jittering.

**Solution**: Added a 'Jitter' slider.

**Implementation**: Added a 'Jitter' slider, it's an important feature for painting and feels great to have it as a slider.

</div>

<div class="feature-section" id="eraser-slider">

## Eraser Slider

**Current State**: New feature.

**Issue**: Eraser size is same as brush size or unique to the eraser.

**Solution**: Added an 'Eraser' slider to work with a custom plug-in that toggles to the eraser tool. The slider value is applied as a scale on the eraser brush size. This allows all the painting tool presets to have a specific sized eraser. Erase pencil lines with a big eraser, cut into brush strokes with a smaller eraser.

**Implementation**: Added an 'Eraser' slider to scale the eraser tool when it is toggled to using a custom Artbox plug-in. Now the painter can pair eraser sizes with tool sizes as part of a tool preset. Erase pencil lines with a big eraser, cut into brush strokes with a smaller eraser. Adjust the relationship as you work to shape the paint and erase the lines effectively, spend less time picking brush sizes.

</div>

<div class="feature-section" id="uniform-jitter">

## Uniform Jitter

**Current State**: New feature.

**Issue**: Jitter has a natural bias towards the center point.

**Solution**: Added an extra option in Additional Options called `Uniform Jitter`. When checked, the jitter is applied in a uniform manner.

**Implementation**: Added an extra option in Additional Options called `Uniform Jitter`. When checked, any jitter is applied in a uniformly distributed way.

</div>

<div class="feature-section" id="initial-angle">

## Initial Angle

**Current State**: New feature.

**Issue**: Needed to go from an initial angle to a directional angle over a fade in length.

**Solution**: Added an extra options in Fade and Colour, one is a slider `Initial Angle` and the other is a checkbox `Fade Initial Angle`. A linear interpolation is done independently of the fade curve according to the fade length.

</div>

<div class="feature-section" id="angle-blend-factor">

## Angle Blend Factor

**Current State**: New feature.

**Issue**: The final blend amount for the linear interpolation can be defined here.

**Solution**: Added an extra options in Fade and Colour, a slider `Brush Angle Blend Factor`.

</div>

<div class="feature-section" id="direction-stabilization">

## Direction Stabilization

**Current State**: New feature.

**Issue**: Delays the start of the stroke until we have some consistent stroke information to work with.

**Solution**: Added an extra options in Fade and Colour, a slider `Direction Stabilization` the pixel distance from the click of the stroke starting to the paint being rendered.

</div>

<div class="feature-section" id="relative-initial-angle">

## Relative Initial Angle

**Current State**: New feature.

**Issue**: Use the initial angle as a relative offset to the direction angle.

**Solution**: Added an extra options in Fade and Colour, `Use Relative Angle`.

</div>

<div class="feature-section" id="random-angle">

## Random Angle

**Current State**: A random angle always added to and angle.

**Issue**: Needed a controllable random amount that could then be used to jitter clockwise and anticlockwise the current angle.

**Solution**: The random curve graph for angles is used to intuitively control this.

**Advanced Details**: Computes the final dynamic brush angle for a paint operation, combining multiple input dynamics (pressure, velocity, direction, tilt, wheel, fade, and random jitter) according to the enabled options and user-defined curves.

Each enabled dynamic contributes an angle value in normalized [0,1) units, where 1.0 == 360°. These values are averaged to produce a base result.

If `Fade Initial Angle` is enabled, the result is smoothly blended from the initial brush angle to the computed dynamic angle over the stroke, using unit vector interpolation for shortest-path blending. The final blend amount can be defined with `Brush Angle Blend Factor`. Check `Use Relative Angle` to apply the initial angle as an offset relative to the active dynamic angle. To avoid an unstable start to the brush stroke, or to turn off the first click stamp, set `Direction Stabilization` to a value greater than 0.

Random angle jitter is applied last, as a small perturbation around the final angle. This is controlled by a user-editable curve in the GUI.

**Usage notes**:

- Enable or disable each dynamic (pressure, velocity, etc.) in the brush dynamics settings.
- Adjust the corresponding input curves to control how each input affects the angle.
- The "fade initial angle" option causes the stroke to start at the initial angle and transition to the dynamic angle as the stroke progresses.
- The random input curve should be centered around 0.5 for symmetric jitter.
- A straight line from 0.0 to 1.0 gives maximum jitter in both directions.
- A flat line at 0.5 gives no jitter.
- A line from 0.4 to 0.6 gives subtle jitter (±0.1 of the maximum).

</div>


