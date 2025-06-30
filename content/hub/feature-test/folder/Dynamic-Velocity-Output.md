---
type: docs
url: "hub/feature-test/folder/Dynamic-Velocity-Output"
---

# Objective

Remove the velocity inversion, so that the dynamic mapping graphs representation is accurate.

## Design Revisions

{{< cards >}}
  {{< card link="#velocity-inversion-removal" title="Remove Velocity Inversion" subtitle="Accurate velocity mapping representation" icon="lightning-bolt" >}}
{{< /cards >}}

---

<div class="feature-section" id="velocity-inversion-removal">

## Remove Velocity Inversion

**Current State**: The velocity calculations are inverted.

**Issue**: The maximum and minimum values are inverted in the spacing curve graph.

**Solution**: The velocity calculations are no longer inverted, and the velocity mapping graph is accurate.

**Implementation**: The velocity is no longer inverted (`1.0 - coords->velocity` removed). `coords->velocity` is mapped directly, making the graph for velocity mapping more accurate.

**Benefits**: This change corrects the velocity mapping in dynamic features, helping users understand and control brush settings without dealing with inverted values.

</div>

---
