---
title: "About"
type: docs
---

Artbox is a digital painting and illustration application for Linux, specifically designed to cater to the needs of artists. It is an open-sourced, artist-adjusted version of GIMP, which allows for more flexibility and customization.  

The intention behind Artbox is to add new features and modify GUI interactions to make the application more fun and productive for artists. While GIMP is a powerful and versatile tool, its broad user base and design requirements can make it difficult to introduce significant changes.  

Artbox addresses this limitation by building on top of the GIMP codebase, adding new features that can do more than traditional plug-ins. However, managing these changes carefully is crucial to ensure that Artbox remains stable and compatible with the underlying GIMP codebase.

**Use at your own risk** When using Artbox, I enable [incremental saving](/artbox/hub/plugins/folder/incremental-save/) and an [auto-save](/artbox/hub/plugins/folder/almost-autosave/). Artbox is designed to use a separate .config folder named 'Artbox'.  

There is an [Artbox Stable](https://gitlab.gnome.org/pixelmixer/artbox-stable/-/commits/artbox?ref_type=heads) repository, which follows GIMP stable releases. However, it is _not_ the same as GIMP stable, as it includes extra features that might reduce stability. It is simply more stable and updated less often than [Artbox Development](https://gitlab.gnome.org/pixelmixer/artbox/-/commits/artbox?ref_type=heads).

Artbox is configured to use a distinct set of data resource folders, separate from GIMP's, to safeguard GIMP assets from being modified by Artbox. For instance, default brushes and dynamics are stored in these dedicated folders. This separation ensures that Artbox maintains its own user data directory under .config and manages its default resource folders independently.

Artbox is powered by the [GNU Image Manipulation Program](https://www.gimp.org/) open source project.

![artbox-logo](/images/artbox-logo.webp)
