# Objective

Enhance the Curve View in the Dynamics Editor and Curves Filter.

## Related Links

- Branches: [Artbox](https://gitlab.gnome.org/pixelmixer/artbox/-/tree/artbox?ref_type=heads)

---

### **Design Revisions**

| **Revision**               | **Current Design**                                           | **Issues**                                                                                             | **Changes**                                                                                               |
|----------------------------|--------------------------------------------------------------|--------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------|
| **1. Grid Line Visibility** | See the Curves Filter or Dynamics Curve graphs | Grid lines in the Curve View are not consistently visible across different background tones.            | Added rendering modes to grid lines, ensuring consistent visibility regardless of the background tone.    |
| **2. Coordinate Display Refinement** | X, Y coordinate display in the Curve View              | The current X, Y coordinate display uses block highlighting, which is visually obtrusive.              | Refined the X, Y coordinate display to avoid block highlighting, improving user experience.               |
| **3. Curve Point Visibility** | Curve points in the Curve View                              | Curve points are difficult to see and select, especially on high-resolution displays (e.g., 4K).        | Enhanced curve point visibility and selection, optimizing for 4K displays and ensuring ease of use.      |
| **4. Shift-Key Curve Movement** | Curve manipulation in the Curve View                      | No mechanism exists to move all curve points simultaneously, limiting flexibility in curve adjustments. | Added a new feature: holding the Shift key allows all curve points to move together, enabling global curve adjustments. |

---

### **Merge Request (MR) Description**

This Merge Request (MR) improves the Curve View in the Dynamics Editor and Curves Filter by addressing visibility issues, refining coordinate displays, and introducing new functionality for more flexible curve manipulation.

#### **Key Changes**

1. **Grid Line Visibility**:
   - Implemented rendering modes for grid lines, ensuring consistent visibility across various background tones in the Curve View.

2. **Refined Coordinate Display**:
   - Redesigned the X, Y coordinate display to eliminate block highlighting, improving readability and reducing visual distraction.

3. **Improved Curve Point Visibility**:
   - Enhanced the visibility and selection of curve points, particularly on high-resolution (e.g., 4K) displays, for a more accessible user experience.

4. **Shift-Key Curve Movement**:
   - Introduced the ability to move all curve points simultaneously by holding down the Shift key, providing a quick and efficient way to adjust the entire curve.

---

### **Benefits**

- **Enhanced Usability**: Consistent grid line visibility and refined coordinate displays make the Curve View easier to interpret and use.
- **Optimized for High Resolution**: Improved curve point visibility ensures seamless usability on 4K displays and beyond.
- **Increased Flexibility**: The new Shift-key feature allows for simultaneous movement of all curve points, enabling efficient global adjustments.
- **Streamlined Workflows**: These changes collectively improve the user experience, making the Dynamics Editor and Curves Filter more intuitive and flexible.

This MR significantly enhances the Curve View by addressing key usability issues and introducing functionality that caters to modern display technologies and advanced editing workflows.
