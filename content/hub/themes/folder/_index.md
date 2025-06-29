---
title: Themes
type: docs
url: "hub/themes/folder"
---

## Introduction

Personalize your experience with custom themes for Artbox and GIMP! Choose from high-contrast options for better visibility, warm palettes for a cozy feel, or dark themes for focused work. These themes are included in Artbox.

Artbox also includes [numerous interface and workflow enhancements](/artbox/hub/feature-test) beyond theming, including improved toolbox layouts, enhanced painting tools, and streamlined resource management.

## Available Themes

{{< cards >}}
  {{< card link="System" title="System Theme" subtitle="Uses CSS styles from your OS for native appearance">}}
  {{< card link="Dark" title="Dark Theme" subtitle="Dark interface for reduced eye strain and focus">}}
  {{< card link="Middle" title="Middle Theme" subtitle="Balanced theme with moderate contrast levels">}}
  {{< card link="Warm" title="Warm Theme" subtitle="Warmer color palette for comfortable working">}}
  {{< card link="High-Contrast" title="High Contrast Theme" subtitle="Enhanced visibility with high contrast elements">}}
{{< /cards >}}

## Installation for GIMP

When Artbox is installed via AppImage or compiled from source, the default theme is the System theme. This theme uses CSS styles from your OS to define the appearance of your GUI. Many system themes can be downloaded, though their quality may vary. Factors like your Linux distribution and Display Manager also influence how system themes work.

These CSS rules are independent of Artbox. Artbox minimally alters the system theme, ensuring continuity with the OS look. Artbox themes, included in the AppImage and compiled versions, are custom CSS styles designed for better usability in Artbox. For a GIMP manual install:

1. [Download](/artbox/downloads/themes.zip)
2. Once the themes.zip has downloaded, extract the themes directory.
3. Select that folder by adding it here: **Edit->Preferences->Folders->Themes**
4. Restart and find the new themes in **Edit->Preferences->Interface->Theme**