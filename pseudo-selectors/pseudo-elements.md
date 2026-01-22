# CSS Pseudo Elements

## : vs ::

| סוג | תחביר | מה זה עושה |
|-----|--------|------------|
| Pseudo Class | `:hover` | מצב של אלמנט קיים |
| Pseudo Element | `::before` | יוצר אלמנט וירטואלי חדש |

---

## ::before / ::after

יוצרים אלמנט וירטואלי **בתוך** האלמנט, לפני/אחרי התוכן.

### content - מה זה עושה?

`content` מגדיר **טקסט או תוכן** שיוצג על המסך:
- `content: 'Hello'` - יציג את הטקסט "Hello"
- `content: ''` - ריק (לשימוש כקישוט גרפי בלבד)
- `content: url(icon.png)` - יציג תמונה

```css
/* adds " before text */
.quote::before {
    content: '"';
}

.quote::after {
    content: '"';
}

/* decorative element */
.title::after {
    content: '';
    display: block;
    width: 50px;
    height: 3px;
    background: blue;
}

/* icon before links starting with https */
/* ^= means "starts with" */
a[href^="https"]::before {
    content: '🔗 ';  /* adds emoji before link text */
}
```

> **חשוב:** בלי `content` האלמנט לא יופיע בכלל! גם אם רוצים רק צורה גרפית, צריך `content: ''`

---

## ::first-letter / ::first-line

```css
/* drop cap effect */
p::first-letter {
    font-size: 3em;
    float: left;
    line-height: 1;
    margin-right: 8px;
}

/* highlight first line */
p::first-line {
    font-weight: bold;
    color: #333;
}
```

---

## ::marker

עיצוב bullets ומספרים ברשימות.

```css
li::marker {
    color: blue;
    font-size: 1.2em;
}

/* custom bullet */
li::marker {
    content: '→ ';
}
```

---

## ::selection

עיצוב טקסט מסומן (כשעושים highlight).

```css
::selection {
    background: #ffeb3b;
    color: black;
}

/* specific element */
p::selection {
    background: purple;
    color: white;
}
```

> מאפיינים שעובדים: `color`, `background`, `text-shadow`

---

## ::placeholder

עיצוב placeholder בשדות input.

```css
input::placeholder {
    color: #999;
    font-style: italic;
}
```

---

## דוגמאות מעשיות

### Badge עם ::after

```css
.new::after {
    content: 'NEW';
    background: red;
    color: white;
    padding: 2px 6px;
    font-size: 0.7em;
    margin-left: 8px;
    border-radius: 3px;
}
```

### ציטוט עם גרשיים

```css
blockquote::before {
    content: '"';
    font-size: 3em;
    color: #ccc;
    position: absolute;
    left: -20px;
    top: -10px;
}

blockquote {
    position: relative;
    padding-left: 30px;
}
```

### קו תחתון מותאם

```css
.underline {
    position: relative;
}

.underline::after {
    content: '';
    position: absolute;
    bottom: 0;
    left: 0;
    width: 100%;
    height: 2px;
    background: linear-gradient(90deg, blue, purple);
}
```

---

## ראה גם

- [pseudo-selectors.md](./pseudo-selectors.md) - Pseudo Classes
- [pseudo-selectors-advanced.md](./pseudo-selectors-advanced.md) - :has(), :not(), :is()
