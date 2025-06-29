---
type: docs
url: "hub/feature-test/folder/Transform-Tool"
---

# Objective

Enhance transforming layers by avoiding GUI rejections and floating layers.

## Design Revisions

| **Revision**                   | **Current Design**                                    | **Issues**                                                        | **Changes**                                            |
|--------------------------------|-------------------------------------------------------|-------------------------------------------------------------------|--------------------------------------------------------|
| **1. Transforming a Layer**       | An active selection is cut and pasted as a floating layer when transformed. The transform is not allowed if the layer and selection area do not overlap. | The selection is often a left over from a previous operation, the user simply wants to transform a layer. | Introduced a 'Use Selection' option on transform tools. If unchecked, the active selection is discarded.|

### Changes

1. **Use Selection**:
  Introduced a 'Use Selection' option on transform tools. If unchecked, the active selection is discarded and the entire layer is transformed.

### **Benefits**

- **Better Workflow**: Users can avoid selections causing errors on transformations and avoid unwanted floating layers.
