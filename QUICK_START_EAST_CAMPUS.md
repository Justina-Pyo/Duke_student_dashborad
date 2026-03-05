# Quick Start - Duke East Campus Dashboard

## 🚀 Get Started in 3 Minutes

### For Your Teammate Who Just Wants to Edit

---

## Step 1: Open the File (30 seconds)

**Option A: Just View It**
- Double-click `duke-dashboard-east-campus.html`
- Opens in browser ✅

**Option B: Edit the Code**
- Right-click → "Open with" → VSCode (or text editor)
- See the code ✅

---

## Step 2: Find the Data (30 seconds)

Press **Ctrl+F** (or Cmd+F on Mac) and search for:

```
BUILDINGS = [
```

You'll see something like this:

```javascript
BUILDINGS = [
  {
    "name": "Alspaugh Hall",
    "capacity": 129,
    "electricity_dec": 731.78,     ← December electricity
    "electricity_jan": 739.91,     ← January electricity
    "electricity_cost_dec": 18294, ← December cost
    "electricity_cost_jan": 17806, ← January cost
    "water_dec": 293727,           ← December water
    "water_jan": 311162,           ← January water
    "water_cost_dec": 18294,
    "water_cost_jan": 17806
  },
  // ... 12 more buildings
];
```

---

## Step 3: Make a Change (2 minutes)

### Example: Update January Electricity

**Before:**
```javascript
"electricity_jan": 739.91,
```

**After:**
```javascript
"electricity_jan": 750.00,
```

**Save** (Ctrl+S) → **Refresh browser** → See the change! ✅

---

## 🎯 What Can You Change?

| Change This | To Do This |
|-------------|------------|
| `electricity_jan` | Update January electricity (MMBtu) |
| `electricity_cost_jan` | Update January electricity cost ($) |
| `water_jan` | Update January water (gallons) |
| `water_cost_jan` | Update January water cost ($) |
| `capacity` | Change # of students |

---

## 📅 Want to Add More Months?

### Three Places to Update:

**1. Add data** (in BUILDINGS array):
```javascript
"electricity_feb": 720.5,
"electricity_cost_feb": 18000,
```

**2. Add dropdown option** (search for `monthSelector`):
```html
<option value="Jan-Feb">Jan 2026 → Feb 2026</option>
```

**3. Add month mapping** (search for `getMonthFields`):
```javascript
'Jan-Feb': { prev: 'Jan', curr: 'Feb', prevLabel: 'January 2026', currLabel: 'February 2026' }
```

---

## 🎨 Want to Change Colors?

Search for: `:root {`

```css
:root {
  --navy: #1A2A6C;  /* Change this */
  --teal: #4DB6AC;  /* And this */
}
```

---

## 🏢 Want to Add a Building?

**1. Add to data:**
```javascript
{
  "name": "New Building",
  "capacity": 150,
  "electricity_dec": 500,
  "electricity_jan": 480,
  // ... add all fields
}
```

**2. Add to map** (search for `HOTSPOT_POSITIONS`):
```javascript
"New Building": { l: 50, t: 50, w: 15, h: 15 }
```

**3. Change "out of 13" to "out of 14"**

---

## ✅ Quick Checklist

Before editing:
- [ ] Made a backup copy

While editing:
- [ ] Save file (Ctrl+S)
- [ ] Refresh browser
- [ ] Check console (F12) for errors

Working?
- [ ] Buildings show on map
- [ ] Data updates when you click
- [ ] Month selector works
- [ ] No red errors in console

---

## 🐛 Something Broke?

### Data shows "—"
→ Check field name spelling (case-sensitive!)

### Can't find section
→ Use Ctrl+F to search

### Browser shows error
→ Press F12, look at Console tab

### Chart doesn't update
→ Make sure you saved the file!

---

## 📞 Need More Help?

- **Detailed guide**: See `CUSTOMIZATION_GUIDE.md`
- **Full docs**: See `README_EAST_CAMPUS.md`
- **Research info**: See `Environmental_Impact_Calculations_Reference.md`

---

## 💡 Pro Tips

1. **Save often** - Ctrl+S after every change
2. **Test in browser** - Refresh to see changes
3. **One change at a time** - Easier to debug
4. **Use search** - Ctrl+F is your friend
5. **Check console** - F12 shows errors

---

**That's it!** 🎉

The entire dashboard is in one HTML file. 
No installation, no servers, no databases.
Just edit, save, and refresh!

---

**Version**: 3.0  
**Buildings**: 13 East Campus  
**File**: duke-dashboard-east-campus.html
