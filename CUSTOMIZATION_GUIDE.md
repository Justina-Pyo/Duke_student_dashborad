# Customization Guide - Step-by-Step Examples

## 🎯 This guide shows exactly how to customize the dashboard with real examples.

---

## 📝 Example 1: Add February 2026 Data

### What You Want:
Add Feb 2026 data and allow comparison of Jan → Feb

### Steps:

**1. Add data to buildings** (find line ~950):

```javascript
{
  "name": "Alspaugh Hall",
  "electricity_jan": 739.91,
  "electricity_cost_jan": 17806,
  // ADD THESE TWO LINES:
  "electricity_feb": 720.5,
  "electricity_cost_feb": 18000,
  
  "water_jan": 311162,
  "water_cost_jan": 17806,
  // ADD THESE TWO LINES:
  "water_feb": 305000,
  "water_cost_feb": 18300,
}
```

**2. Add to month selector** (find line ~730):

```html
<select id="monthSelector">
  <option value="Dec-Jan">Dec 2025 → Jan 2026</option>
  <option value="Nov-Dec">Nov 2025 → Dec 2025</option>
  <!-- ADD THIS LINE: -->
  <option value="Jan-Feb">Jan 2026 → Feb 2026</option>
</select>
```

**3. Update month mapping** (find line ~1055):

```javascript
function getMonthFields() {
  const monthMap = {
    'Dec-Jan': { prev: 'Dec', curr: 'Jan', prevLabel: 'December 2025', currLabel: 'January 2026' },
    // ADD THIS LINE:
    'Jan-Feb': { prev: 'Jan', curr: 'Feb', prevLabel: 'January 2026', currLabel: 'February 2026' },
  };
  return monthMap[currentMonthComparison] || monthMap['Dec-Jan'];
}
```

**4. Save and test!**
- Save file
- Refresh browser
- Select "Jan 2026 → Feb 2026" from dropdown
- Should show Feb data!

---

## 🎨 Example 2: Change to UNC Colors

### What You Want:
Change from Duke blue to Carolina blue

### Steps:

**Find CSS variables** (line ~20):

```css
/* BEFORE (Duke colors): */
:root {
  --navy:    #1A2A6C;
  --teal:    #4DB6AC;
}

/* AFTER (UNC colors): */
:root {
  --navy:    #7BAFD4;  /* Carolina blue */
  --teal:    #13294B;  /* Navy blue */
}
```

**Save and refresh** - entire dashboard updates!

---

## 🏢 Example 3: Add a 14th Building

### What You Want:
Add "Crowell Quad" to East Campus

### Steps:

**1. Add building data** (in BUILDINGS array, line ~950):

```javascript
BUILDINGS = [
  { name: "Bassett Hall", ... },
  { name: "West Hall", ... },
  // ADD THIS ENTIRE BLOCK:
  {
    "name": "Crowell Quad",
    "capacity": 180,
    "electricity_dec": 650.0,
    "electricity_jan": 620.0,
    "electricity_cost_dec": 16250,
    "electricity_cost_jan": 15500,
    "water_dec": 450000,
    "water_jan": 440000,
    "water_cost_dec": 27000,
    "water_cost_jan": 26400,
    // Add all other months too...
  }
];
```

**2. Add map hotspot** (line ~920):

```javascript
const HOTSPOT_POSITIONS = {
  "West Hall": { l: 63, t: 70, w: 12, h: 15 },
  // ADD THIS LINE:
  "Crowell Quad": { l: 45, t: 55, w: 18, h: 16 },
};
```

**3. Update "out of 13" text**:

Search for: `out of 13`
Replace with: `out of 14`

(Appears in 2 places - stat card label and unit text)

**4. Save and test!**

---

## 💰 Example 4: Change Electricity Rate

### What You Want:
Update from $25/MMBtu to $30/MMBtu

### Option A: Update Estimated Costs (Easy)

Search for: `* 25` in the JavaScript section

```javascript
// BEFORE:
b[`electricity_cost_${month_lower}`] = round(value * 25, 2)

// AFTER:
b[`electricity_cost_${month_lower}`] = round(value * 30, 2)
```

### Option B: Update Actual Costs (Precise)

Manually change each cost value in the data:

```javascript
"electricity_cost_dec": 21960,  // Was 18300, now 731.78 × 30
"electricity_cost_jan": 22197,  // Was 18496, now 739.91 × 30
```

---

## 📅 Example 5: Show Different Default Month

### What You Want:
Open dashboard to "Nov → Dec" instead of "Dec → Jan"

### Steps:

**1. Change selected option** (line ~730):

```html
<!-- BEFORE: -->
<option value="Dec-Jan" selected>Dec 2025 → Jan 2026</option>
<option value="Nov-Dec">Nov 2025 → Dec 2025</option>

<!-- AFTER: -->
<option value="Dec-Jan">Dec 2025 → Jan 2026</option>
<option value="Nov-Dec" selected>Nov 2025 → Dec 2025</option>
```

**2. Update initial state** (line ~910):

```javascript
// BEFORE:
let currentMonthComparison = 'Dec-Jan';

// AFTER:
let currentMonthComparison = 'Nov-Dec';
```

---

## 🔢 Example 6: Change Water Rate

### What You Want:
Update from $0.06/gallon to $0.08/gallon

### Steps:

Search for: `* 0.06`

```javascript
// BEFORE:
b[`water_cost_${month_lower}`] = round(water_value * 0.06, 2);

// AFTER:
b[`water_cost_${month_lower}`] = round(water_value * 0.08, 2);
```

Or manually update water costs in the data.

---

## 🎯 Example 7: Add Building Notes

### What You Want:
Add a note showing when building was renovated

### Steps:

**1. Add note field to data**:

```javascript
{
  "name": "Bassett Hall",
  "capacity": 187,
  "note": "Renovated 2022",  // ADD THIS
  // ... rest of data
}
```

**2. Display in building header** (find `selectBuilding`, line ~1025):

```javascript
// After line that sets bhMeta:
document.getElementById('bhMeta').textContent = 
  `${building.capacity} students · ${building.note || 'Electricity Data (Dec-Jan 2026)'}`;
```

---

## 📊 Example 8: Add Annual Total Display

### What You Want:
Show total annual costs for each building

### Steps:

**1. Calculate annual total** (in `renderMeterChart`, line ~1060):

```javascript
// After calculating totalCost:
const annualElec = Object.keys(selectedBuilding)
  .filter(k => k.startsWith('electricity_cost_'))
  .reduce((sum, k) => sum + (selectedBuilding[k] || 0), 0);

const annualWater = Object.keys(selectedBuilding)
  .filter(k => k.startsWith('water_cost_'))
  .reduce((sum, k) => sum + (selectedBuilding[k] || 0), 0);

const annualTotal = annualElec + annualWater;
```

**2. Display it**:

Add a new stat card or update existing one:

```javascript
document.getElementById('meterTotalCost').textContent = 
  `Annual: $${annualTotal.toLocaleString('en-US', {maximumFractionDigits: 0})}`;
```

---

## 🔍 Example 9: Find Specific Code Sections

### What to Search For:

| Want to Change | Search For |
|----------------|------------|
| Building data | `BUILDINGS = [` |
| Electricity values | `electricity_` |
| Water values | `water_` |
| Costs | `_cost_` |
| Colors | `:root {` |
| Month dropdown | `id="monthSelector"` |
| Month mapping | `getMonthFields()` |
| Display update | `renderMeterChart()` |
| Map hotspots | `HOTSPOT_POSITIONS` |

---

## ✅ Testing Checklist

After making any change:

- [ ] Save the file
- [ ] Refresh browser (Ctrl+Shift+R for hard refresh)
- [ ] Open browser console (F12)
- [ ] Check for any red errors
- [ ] Click through different buildings
- [ ] Try different months
- [ ] Toggle electricity/water
- [ ] Verify calculations look correct

---

## 🐛 Common Mistakes & Fixes

### Mistake 1: Missing Comma
```javascript
// WRONG:
{
  "name": "Hall"
  "capacity": 150  // Missing comma above!
}

// RIGHT:
{
  "name": "Hall",
  "capacity": 150
}
```

### Mistake 2: Wrong Field Names
```javascript
// WRONG:
"elec_dec": 500,  // Should be electricity_dec

// RIGHT:
"electricity_dec": 500,
```

### Mistake 3: Mismatched Months
```javascript
// In month selector:
<option value="Jan-Feb">

// But in getMonthFields:
'Feb-Jan': { ... }  // WRONG ORDER!

// Should be:
'Jan-Feb': { ... }  // CORRECT!
```

---

## 💡 Pro Tips

1. **Make one change at a time** - easier to debug
2. **Use browser DevTools** - F12 shows errors
3. **Keep a backup** - copy file before major edits
4. **Test in browser** - after every change
5. **Use search** - Ctrl+F to find sections quickly
6. **Beautify code** - VSCode can auto-format
7. **Check console** - catch errors early
8. **Comment changes** - add `// Changed on 2/26/26`

---

## 📞 Quick Reference

### File Locations in Code:
- Line ~20: CSS color variables
- Line ~730: Month selector dropdown
- Line ~910: JavaScript variables
- Line ~920: Map hotspot positions
- Line ~950: Building data (BUILDINGS array)
- Line ~980: Research actions
- Line ~1025: Building selection handler
- Line ~1045: Month change handler
- Line ~1055: Month field mapping
- Line ~1060: Main render function

### Common Values:
- Electricity rate: $25/MMBtu
- Water rate: $0.06/gallon
- Default month: Dec-Jan
- Number of buildings: 13
- Months available: 12 (full year)

---

**Happy Customizing!** 🎉

*Remember: The dashboard is self-contained. All changes happen in one HTML file!*
