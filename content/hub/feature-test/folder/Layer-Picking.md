---
type: docs
url: "hub/feature-test/folder/Layer-Picking"
---

# Layer Picking

Improve the layer picking experience in a complex scene.

## Design Revisions

{{< cards >}}
  {{< card link="#alt-key-layer-picking" title="Alt Key Layer Picking" subtitle="Quick layer selection beneath cursor" icon="hand" >}}
{{< /cards >}}

---

<div class="feature-section" id="alt-key-layer-picking">

## Alt Key Layer Picking

**Current State**: Repurposed Feature, existed as configurable modifier that also needed a button click. Perhaps `Alt middle mouse button` is the default.

**Issue**: Unable to use the existing modifier set up easily with a stylus, modifier customization has issues.

**Solution**: When Alt is pressed, on _release_ a layer beneath the cursor is selected. There may be more than one layer, on the next press and release pick the next layer, and so on. If a button is pressed, left click or right click, during the Alt press then the pick does not happen on Alt release. If another key is pressed, during the Alt press then the pick does not happen on Alt release.

**Benefits**: The user can tap the Alt key to pick layers beneath the cursor, the status bar shows the name of the layer picked and it is also highlighted in the layer stack. There is a white handle drawn on the view to indicate the layer center point. This handle diminishes and fades as the cursor is moved. Alt dragging should work as normal to increase brush size, there may be other Alt conflicts to resolve, let me know! The existing code was fine but awkward to use, this change puts it front and center as a way to work with the layer stack in complex scenes. Tap Alt over a set of layers to cycle through them as active layer selections.

</div>

---
