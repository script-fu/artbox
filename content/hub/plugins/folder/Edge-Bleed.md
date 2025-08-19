---
title: Edge Bleed
type: docs
url: "hub/plugins/folder/Edge-Bleed"
---

## Introduction

Extends edge pixels into transparent areas using distance field propagation. The filter creates solid alpha padding around image content, eliminating transparent halos in compositing operations. The Script-Fu plug-in also calls a custom GEGL plug-in for speed.

[YouTube-video-demo](https://youtu.be/0aZzneEOLa8)

### Parameters

- **bleed**              — bleed distance (1-32 pixels)
- **alpha-threshold**    — Alpha threshold for detecting transparent regions

### Plug-in Menu Location

_Filters -> > Edge-Detect > Edge Bleed_