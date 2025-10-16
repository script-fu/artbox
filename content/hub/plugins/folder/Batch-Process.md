---
title: Batch Process
type: docs
url: "hub/plugins/folder/Batch-Process"
---

## Introduction

A flexible batch processing framework for Script-Fu that processes multiple images from a directory. This plug-in lets you format in a scripted manner, an entire directory of XCF images, including those in nested folders, and save the results to a customized destination folder.

**Key Features:**

- Process files from disk or open images
- Recursive directory processing with file discovery
- Customizable processing and export functions
- ICC color profile support for CMYK export
- Proper display and image lifecycle management
- Progress reporting during batch operations

### Plug-in Menu Location

_File -> Batch Process_

### Quick Setup

Configure these values at the top of the batch-process.scm file:

- **`default-src-dir`** - Your default source directory
- **`default-dst-dir`** - Your default destination directory
- **`softproof-icc`** - Path to your ICC color profile (optional)

### Processing Modes

1. **File System Mode** - Process files from a source directory
2. **Open Image Mode** - Process currently open image(s)

The example processing function creates 50% scaled versions with sharpening applied—ideal for creating web/social media versions from high-res originals.

### Keyboard Shortcut

This forces Artbox to save the shortcut for the next session. First, search for the plug-in name, and assign a shortcut.

_Edit > Keyboard Shortcuts_

Once the shortcut is working as you like, save your work then;

_File > Quit_
