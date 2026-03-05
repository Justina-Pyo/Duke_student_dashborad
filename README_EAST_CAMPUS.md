# Duke East Campus Energy Dashboard - Complete Guide

## 📊 Project Overview

Interactive dashboard tracking electricity & water consumption across 13 Duke East Campus residence halls with real-time cost analysis, multi-month comparisons, and environmental impact calculations.

**KEY FEATURES:**
- ✅ Multi-month selector (5 month pairs)
- ✅ Electricity + Water dual display
- ✅ Real cost data with $ amounts
- ✅ Dynamic rankings per month
- ✅ 48 data points per building

---

## 🏢 East Campus Buildings (13)

Trinity | Bell Tower | Southgate | Gilbert-Addoms | Blackwell | Randolph | Pegram | Bassett | **Alspaugh (real data)** | Brown | Giles | Wilson | West Hall

---

## 🚀 Quick Start for Your Teammate

### Just Open It:
1. Double-click `duke-dashboard-east-campus.html`
2. Works in any modern browser!

### To Edit:
1. Open in text editor (VSCode recommended)
2. Find `BUILDINGS = [` (around line 950)
3. Change values, save, refresh browser

---

## 🔧 Most Common Edits

### ✏️ Edit 1: Update Monthly Data

Search for: `BUILDINGS = [`

```javascript
{
  "name": "Alspaugh Hall",
  "electricity_dec": 731.78,      // ← December consumption (MMBtu)
  "electricity_jan": 739.91,      // ← January consumption
  "electricity_cost_dec": 18294,  // ← December cost ($)
  "electricity_cost_jan": 17806,  // ← January cost ($)
  "water_dec": 293727,            // ← Water (gallons)
  "water_jan": 311162,
  "water_cost_dec": 18294,        // ← Water cost ($)
  "water_cost_jan": 17806
}
```

### 📅 Edit 2: Add New Month

**Step 1:** Add to dropdown (line ~730):
```html
<option value="Feb-Mar">Feb 2026 → Mar 2026</option>
```

**Step 2:** Add to month mapping (line ~1050):
```javascript
'Feb-Mar': { prev: 'Feb', curr: 'Mar', prevLabel: 'February 2026', currLabel: 'March 2026' }
```

**Step 3:** Add data to buildings:
```javascript
"electricity_feb": 720.5,
"electricity_cost_feb": 18000,
"water_feb": 305000,
"water_cost_feb": 18300
```

### 🎨 Edit 3: Change Colors

Find `:root {` (line ~20):
```css
--navy: #1A2A6C;  /* Change to your school color */
--teal: #4DB6AC;  /* Accent color */
```

### 🏢 Edit 4: Add Building

Add to BUILDINGS array + HOTSPOT_POSITIONS (see full README for details)

---

## 📊 Data Structure

Each building has **48 data points**:
- 12 months × 2 utilities (elec/water) × 2 metrics (consumption/cost)

```javascript
{
  "name": "Building Name",
  "capacity": 150,
  
  // Electricity (12 months)
  "electricity_jan": 500.0,  // MMBtu
  "electricity_feb": 485.0,
  // ... through dec
  
  // Electricity costs (12 months)  
  "electricity_cost_jan": 12500,  // $
  "electricity_cost_feb": 12100,
  // ... through dec
  
  // Water (12 months)
  "water_jan": 350000,  // gallons
  "water_feb": 340000,
  // ... through dec
  
  // Water costs (12 months)
  "water_cost_jan": 21000,  // $
  "water_cost_feb": 20400
  // ... through dec
}
```

---

## 🎯 Key Functions (for editing)

| Function | Line | Purpose |
|----------|------|---------|
| `boot()` | ~950 | Loads all data |
| `changeMonthComparison()` | ~1045 | Handles month selector |
| `switchUtilityType()` | ~1050 | Toggles elec/water |
| `getMonthFields()` | ~1055 | Maps month pairs |
| `renderMeterChart()` | ~1060 | Updates display |

---

## 🐛 Troubleshooting

| Problem | Solution |
|---------|----------|
| Data shows "—" | Check field names match exactly |
| Wrong month | Verify `getMonthFields()` mapping |
| Rankings wrong | Check all buildings have data for month |
| Costs wrong | Check `_cost_` fields in data |

---

## 📧 How to Share

1. **Email** - just attach the HTML file
2. **Google Drive** - upload & share link  
3. **GitHub** - push to repo, enable Pages
4. **USB** - copy file to drive

---

## ✅ Teammate Checklist

Before editing:
- [ ] Made backup copy
- [ ] Opened in code editor
- [ ] Located BUILDINGS array

When editing:
- [ ] Save frequently
- [ ] Test in browser
- [ ] Check console (F12)

After editing:
- [ ] All buildings visible
- [ ] Rankings work
- [ ] No errors

---

## 📚 Resources

- Full README with examples: See this file
- Research sources: `Environmental_Impact_Calculations_Reference.md`
- Quick start: `QUICK_START_EAST_CAMPUS.md`

**Version 3.0** - Multi-Month Edition  
**Last Updated**: Feb 26, 2026

*Self-contained, no installation needed!*
