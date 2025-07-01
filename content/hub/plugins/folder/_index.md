---
title: Plugins
type: docs
url: "hub/plugins/folder"
---

## Introduction

Some of these plugins are exclusive to Artbox, as they use additional commands not available in GIMP. They are generally written using Script-Fu, a Scheme based scripting language that is part of GIMP. They install as part of Artbox to the data resource folders when it is built locally, or can be found bundled in the AppImage download.

If you wish to deactivate these plugins you can do so by changing your preferences in Artbox.

Edit -> Preferences -> Folders -> Plug-ins

Remove the `share/artbox/` path.

## Paint Tool Utilities

{{< cards >}}
  {{< card link="Toggle-Paint-Mode" title="Toggle Paint Mode" subtitle="Switch between paint and erase modes using the eraser slider value">}}
  {{< card link="Toggle-Paintbrush-Eraser" title="Toggle Paintbrush Eraser" subtitle="Quick toggle between paintbrush and eraser tools">}}
  {{< card link="Toggle-Eraser" title="Toggle Eraser" subtitle="Alternative eraser toggle functionality">}}
  {{< card link="Add-Path-Guide" title="Add Path Guide" subtitle="Creates a locked path guide for drawing straight lines and curves">}}
{{< /cards >}}

## Layer Management

{{< cards >}}
  {{< card link="Layer-Group" title="Group Selected Layers" subtitle="Creates a new layer group from selected layers">}}
  {{< card link="Layer-Group-To-New-Image" title="Layer Group To New Image" subtitle="Exports layer groups as new image files">}}
  {{< card link="New-Layer-From-Selection" title="New Layer From Selection" subtitle="Creates a new layer from the current selection">}}
  {{< card link="Rename-Layers" title="Rename Layers" subtitle="Batch rename multiple layers with pattern options">}}
{{< /cards >}}

## File Management

{{< cards >}}
  {{< card link="Incremental-Save" title="Incremental Save" subtitle="Saves numbered versions to a subfolder without overwriting the original">}}
  {{< card link="Almost-Autosave" title="Almost Autosave" subtitle="Automated saving functionality for workflow protection">}}
{{< /cards >}}

## Effects & Utilities

{{< cards >}}
  {{< card link="Gaussian-Glow" title="Gaussian Glow" subtitle="Multi-layered glow effect with successive blurs and opacity control">}}
  {{< card link="Alpha-To-Show-Mask" title="Alpha To Show Mask" subtitle="Converts alpha channel information to visible mask display">}}
{{< /cards >}}

### Related Sites

- [Funky-Fu](https://script-fu.github.io/funky/)  
- [GIMP documentation](https://docs.gimp.org/en/gimp-concepts-script-fu.html)  
- [Scheme](https://www.scheme.org/)