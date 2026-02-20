# Debug Report: javaerror.html

## Summary
Fixed CSS syntax error in the javaerror.html file that was preventing proper parsing of the stylesheet.

---

## Error Found

**File:** `javaerror.html`  
**Line:** 173  
**CSS Rule:** `.file-btn`

### The Problem
```css
.file-btn {
    font - size: 0.75rem;  /* ❌ ERROR: Spaces around hyphen */
    padding: 5px 10px;
    background: #222;
    border-radius: 10px;
    cursor: pointer;
    border: 1px solid #333;
    max-width: 100px;
    overflow: hidden;
    text-overflow: ellipsis;
    white-space: nowrap;
}
```

The property `font - size` has **spaces around the hyphen**, which breaks the CSS syntax. CSS property names cannot have spaces around the hyphen separator.

### Compiler Errors Generated
- `semi-colon expected`
- `colon expected`
- `{ expected` (cascading errors in subsequent properties)

These errors cascaded because the CSS parser couldn't recognize the malformed property, breaking the entire rule.

---

## Solution Applied

**Changed:** `font - size: 0.75rem;`  
**To:** `font-size: 0.75rem;`

### The Fixed Code
```css
.file-btn {
    font-size: 0.75rem;  /* ✅ FIXED: No spaces around hyphen */
    padding: 5px 10px;
    background: #222;
    border-radius: 10px;
    cursor: pointer;
    border: 1px solid #333;
    max-width: 100px;
    overflow: hidden;
    text-overflow: ellipsis;
    white-space: nowrap;
}
```

---

## Why This Error Occurred

CSS property names use hyphens as part of their syntax (e.g., `font-size`, `background-color`, `max-width`). These hyphens are **mandatory parts of the property name** and cannot have spaces around them.

### Common CSS Properties with Hyphens:
- `font-size`
- `background-color`
- `border-radius`
- `text-align`
- `max-width`
- `overflow-y`
- `box-shadow`

---

## Validation

After the fix, all CSS syntax errors in the file were resolved. The stylesheet now parses correctly without any compiler errors.

---

## Lesson Learned

Always ensure CSS property names are spelled correctly without spaces around hyphens. Common patterns to watch for:
- ❌ `font - size` → ✅ `font-size`
- ❌ `background - color` → ✅ `background-color`
- ❌ `text - align` → ✅ `text-align`
