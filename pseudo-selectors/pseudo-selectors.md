# CSS Pseudo Selectors

## nth-child vs nth-of-type

> **nth-child** - סופר את **כל הילדים**
> 
> **nth-of-type** - סופר רק ילדים **מאותו סוג**

```html
<div>
    <h2>Title</h2>   <!-- child #1, h2 #1 -->
    <p>First</p>     <!-- child #2, p #1 -->
    <p>Second</p>    <!-- child #3, p #2 -->
</div>
```

| סלקטור | תוצאה | הסבר |
|--------|-------|------|
| `p:nth-child(2)` | ✅ "First" | הילד ה-2 (והוא אכן p) |
| `p:nth-of-type(2)` | ✅ "Second" | ה-p ה-2 (מתעלם מה-h2) |
| `p:first-child` | ❌ כלום | מחפש p שהוא ילד ראשון, אבל הראשון הוא h2 |
| `p:first-of-type` | ✅ "First" | ה-p הראשון (לא משנה מה לפניו) |

**כלל אצבע:** כשיש ספק, השתמש ב-`of-type` - הוא צפוי יותר.

---

## סלקטורי מיקום

### Child-based

```css
li:first-child { }
li:last-child { }
li:nth-child(3) { }
li:only-child { }
```

### Type-based

```css
p:first-of-type { }
p:last-of-type { }
p:nth-of-type(3) { }
p:only-of-type { }
```

### נוסחאות nth

```css
tr:nth-child(even) { }     /* 2, 4, 6... */
tr:nth-child(odd) { }      /* 1, 3, 5... */
li:nth-child(3n) { }       /* 3, 6, 9... */
li:nth-child(3n+1) { }     /* 1, 4, 7... */
```

---

## סלקטורי אינטראקציה

```css
a:hover { }
button:active { }
input:focus { }
button:focus-visible { }   /* focus from keyboard only */
```

---

## סלקטורי טפסים

```css
input:checked { }
button:disabled { }
button:enabled { }
input:required { }
input:optional { }
input:valid { }
input:invalid { }
input:placeholder-shown { }
input:read-only { }
```

---

## Combinators

```css
ul > li { }    /* direct child */
ul li { }      /* descendant */
h2 + p { }     /* adjacent sibling */
h2 ~ p { }     /* general sibling */
```

---

## דוגמה: טבלה מפוספסת

```css
table {
    width: 100%;
    border-collapse: collapse;
}

thead tr {
    background-color: #333;
    color: white;
}

tbody tr:nth-of-type(odd) {
    background-color: #f9f9f9;
}

tbody tr:hover {
    background-color: #e0e0e0;
}

td:first-of-type {
    font-weight: bold;
}
```

---

## ראה גם

- [pseudo-elements.md](./pseudo-elements.md) - `::before`, `::after`, `::marker`
- [pseudo-selectors-advanced.md](./pseudo-selectors-advanced.md) - `:has()`, `:not()`, `:is()`, `:where()`
