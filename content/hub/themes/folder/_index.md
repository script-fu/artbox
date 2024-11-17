---
title: Themes
type: docs
---

## Introduction

Personalize your experience with custom themes for GIMP and Artbox! Choose from high-contrast options for better visibility, warm palettes for a cozy feel, or dark themes for focused work. These themes are easy to install, compatible with multiple platforms, and let you customize the Artbox interface to your style.

When Artbox is installed via AppImage or compiled from source, the default theme is the System theme. This theme uses CSS styles from your OS to define the appearance of your GUI. Many system themes can be downloaded, though their quality may vary. Factors like your Linux distribution and Display Manager also influence how system themes work.

These CSS rules are independent of Artbox. Artbox minimally alters the system theme, ensuring continuity with the OS look. Pixelmixer themes, included in the AppImage and compiled versions, are custom CSS styles designed for better usability in Artbox. For GIMP, these themes can be installed as follows:

1. [Download](/artbox/downloads/themes.zip)
2. Once the themes.zip has downloaded, extract the themes directory.
3. Point Artbox at that folder by adding it here: **Edit->Preferences->Folders->Themes**
4. Restart Artbox and find the new themes in **Edit->Preferences->Interface->Theme**

### Themes Structure

Inside the default theme folder are CSS files and assets. Color definitions for the theme are in 'color-definitions.css'. Assets for a theme are in the assets folder, they are assigned by the CSS file 'color.css' in the 'stylesheets' folder. The stylesheets folder contains:

* **Color**: assignments for color, borders and opacity.
* **Layout**: assignments for margins, padding and sizing.
* **Font**: assignments for size, style and weight.
* **Round**: assignments for rounded corners.
