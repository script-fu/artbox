---
title: Incremental Save
type: docs
url: "hub/plugins/folder/Incremental-Save"
---

## Introduction

This is an incremental save feature. It saves a numbered version of the active file into a named sub-folder. It does not save over the opened file. Each image can have a unique number of saves, before the saves wrap around. Useful to save stages of progress, before committing to a proper save. Also good for recovering an earlier version.

### Save Folder and File Structure

* Image Folder
  * FileName_saves
    * FileName_1.xcf
    * FileName_2.xcf
    * FileName_3.xcf
    ...

### Plug-in Menu Location

_File -> Incremental Save_
