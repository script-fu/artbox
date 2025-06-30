---
type: docs
url: "hub/feature-test/folder/Tool-Tips"
---

# Tool Tips

Improve the quality of the user interface experience by optionally deactivating distracting tool tips.

{{< cards >}}
  {{< card link="#configurable-tooltips" title="Configurable Tooltips" subtitle="Toggle tooltip display on/off" icon="information-circle" >}}
{{< /cards >}}

---

<div class="feature-section" id="configurable-tooltips" tabindex="-1">

## Configurable Tooltips

**Current Design**: Tooltips cannot be turned off

**Issues**: Users cannot stop distracting tips from flickering on and off

**Changes**: Introduced a new Preferences option, `Show tool tips`, allowing users to toggle some tooltips on or off.

**Implementation**:
- Added a new `show_tool_tips` property to the `GimpGuiConfig` structure, making tooltip display configurable through the codebase.
- Integrated the tooltip preference under `Preferences -> Interface -> Help System -> General -> Show tool tips`, allowing users to toggle tooltip visibility easily within the UI.

**Benefits**: The addition of the `show_tool_tips` option enhances user control over the interface, reducing UI clutter for users who prefer minimal tool guidance, while retaining tooltip functionality for those who rely on detailed tool descriptions. Though primarily a workaround to reduce tooltip distractions, a more granular solution could be implemented for further customization.

</div>


