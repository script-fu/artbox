---
type: docs
url: "hub/docs/folder/Data"
---

# What is Artbox Data?

Artbox includes a customized data repository that extends GIMP's default resources with:

- **New Splash Screen**: Custom startup screen for Artbox
- **Extended Icons**: Additional icon sets beyond GIMP's defaults

## How It Works

The Artbox data is managed as a **submodule** - a separate repository that's linked to the main Artbox project:

- **Synchronized Updates**: Data stays in sync with Artbox releases
- **GIMP Compatibility**: Built on GIMP's data structure for seamless integration
- **Version Control**: Each Artbox version references a specific data snapshot

## Benefits for Users

### What It Provides
The Artbox data repository includes:
- A custom splash screen displayed at startup
- Additional icon collections for the interface
- Necessary data files that support Artbox features

### Management
- The data is maintained as a separate repository
- It needs to be kept synchronized with Artbox releases
- Each Artbox version references a specific data snapshot

## Technical Details

For developers and advanced users:

- **Repository**: The data is maintained separately at [Artbox Data Repository](https://gitlab.gnome.org/pixelmixer/artbox-data)
- **Integration**: Linked as a Git submodule in the main Artbox build
- **Updates**: Regularly synchronized with upstream GIMP data while preserving Artbox enhancements

The data repository ensures that Artbox has the resources it needs while staying compatible with GIMP's data structure.
