---
type: docs
url: "hub/feature-test/folder/Transform-Tool"
---

# Objective

Enhance transforming layers by avoiding GUI rejections and floating layers.

## Design Revisions

{{< cards >}}
  {{< card link="#use-selection-option" title="Use Selection Option" subtitle="Better layer transformation workflow" icon="switch-horizontal" >}}
{{< /cards >}}

---

<div class="feature-section" id="use-selection-option">

## Use Selection Option

**Current State**: An active selection is cut and pasted as a floating layer when transformed. The transform is not allowed if the layer and selection area do not overlap.

**Issue**: The selection is often a left over from a previous operation, the user simply wants to transform a layer.

**Solution**: Introduced a 'Use Selection' option on transform tools. If unchecked, the active selection is discarded.

**Implementation**: Introduced a 'Use Selection' option on transform tools. If unchecked, the active selection is discarded and the entire layer is transformed.

**Benefits**: Users can avoid selections causing errors on transformations and avoid unwanted floating layers.

</div>

---
