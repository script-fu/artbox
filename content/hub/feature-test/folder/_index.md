---
title: Feature Testing
type: docs
url: "hub/feature-test/folder"
---

## Introduction

Artbox extends GIMP with numerous enhancements focused on digital art workflows, interface improvements, and painting tool optimizations. These experimental features may be subject to change or refinement based on user feedback.

## Core Painting Improvements

{{< cards >}}
  {{< card link="Paint-Tool" title="Paint Tool Enhancements" subtitle="Cursor visibility improvements, erase mode indicators, simple brush boundaries, and mask-aware erasing for better painting feedback">}}
  {{< card link="Paintbrush-Options" title="Paintbrush Options" subtitle="GUI reorganization with optional buttons, new sliders for jitter and eraser, and additional stroke controls">}}
  {{< card link="Paintbrush-High-Quality-Force" title="High Quality Force" subtitle="Enables existing high quality pressure handling that was disabled for performance reasons">}}
  {{< card link="Paintbrush-Smooth-Stroke" title="Smooth Stroke" subtitle="Position, pressure, and direction smoothing with renamed controls for clarity">}}
{{< /cards >}}

## Brush & Dynamics Systems

{{< cards >}}
  {{< card link="Dynamic-Brush-Spacing" title="Dynamic Brush Spacing" subtitle="Removes spacing limits to respect paint tool slider settings">}}
  {{< card link="Brush-Aspect-Ratio-Range" title="Brush Aspect Ratio" subtitle="Normalized linear range from -1 to 1 replacing the old non-linear system">}}
  {{< card link="Dynamics-Editor" title="Dynamics Editor" subtitle="Scrollable matrix, improved labels, and copy/paste curve functionality">}}
  {{< card link="Dynamic-Velocity-Output" title="Velocity Output" subtitle="Removes velocity inversion to make mapping graphs accurate">}}
{{< /cards >}}

## Advanced Dynamics Control

{{< cards >}}
  {{< card link="Dynamic-Multiply-Modes" title="Multiply Modes" subtitle="Extended operation modes for complex brush behaviors">}}
  {{< card link="Dynamic-Velocity-Compression" title="Velocity Compression" subtitle="Fine-tuned response management for precise control">}}
{{< /cards >}}

## Tool Enhancements

{{< cards >}}
  {{< card link="Filter-Restores-Last-Tool" title="Filter Tool Restore" subtitle="Auto-restore previous tool after filters">}}
  {{< card link="Transform-Tool" title="Transform Tool" subtitle="Selection override options">}}
  {{< card link="Path-Tool" title="Path Tool" subtitle="Enhanced path editing capabilities">}}
  {{< card link="Color-Picker-Tool" title="Color Picker" subtitle="Improved color sampling accuracy">}}
  {{< card link="Warp-Tool" title="Warp Tool" subtitle="Enhanced warping capabilities for layer groups">}}
{{< /cards >}}

## Interface & Workflow Enhancements

{{< cards >}}
  {{< card link="Toolbox" title="Toolbox Improvements" subtitle="Optional flowbox removal and configurable foreground/background widget positioning">}}
  {{< card link="Fullscreen" title="Fullscreen Mode" subtitle="True fullscreen with dock hiding">}}
  {{< card link="Simple-Sliders" title="Simple Sliders" subtitle="Click-to-slide behavior and simplified cursor icons">}}
  {{< card link="Selection-Display" title="Selection Display" subtitle="Enhanced selection highlighting">}}
  {{< card link="Selection" title="Selection Tools" subtitle="Enhanced selection manipulation">}}
{{< /cards >}}

## Resource & Preset Management

{{< cards >}}
  {{< card link="Resource-Control" title="Resource Control" subtitle="Optional auto-save, immediate save options, and improved resource handling workflows">}}
  {{< card link="Presets-Restore" title="Presets Restore" subtitle="Enhanced preset management functionality">}}
  {{< card link="Tool-Preset-Editor" title="Tool Preset Editor" subtitle="Larger icon picker and tool preset information table">}}
{{< /cards >}}

## Interface Utilities

{{< cards >}}
  {{< card link="Curves-View" title="Curves View" subtitle="Enhanced curve editing with improved grid visibility">}}
  {{< card link="Layer-Picking" title="Layer Picking" subtitle="Improved layer selection workflow">}}
  {{< card link="Tool-Tips" title="Tool Tips" subtitle="Enhanced contextual help system">}}
{{< /cards >}}

## Scripting & Automation

{{< cards >}}
  {{< card link="Script-Fu" title="Script-Fu Extensions" subtitle="Additional automation functions for workflow enhancement">}}
{{< /cards >}}

## Related Sites

[Design Proposals for Digital Art](https://gitlab.gnome.org/americo_gobbo/GIMPBrushwork/-/boards)

![beep-beep](/images/gallery/red-rock_final.webp)