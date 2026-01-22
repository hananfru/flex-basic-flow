# CSS Pseudo Selectors - מתקדם

> ראה גם: [pseudo-elements.md](./pseudo-elements.md) - `::before`, `::after`, `::marker`

## :not() - שלילה

בוחר אלמנטים שלא מתאימים לסלקטור.

```css
/* all links except hovered */
a:not(:hover) { opacity: 0.8; }

/* all children except first */
li:not(:first-child) { border-top: 1px solid #ddd; }

/* can combine multiple */
input:not(:disabled):not(:read-only) { }
```

---

## :has() - בחירת הורה לפי ילד

> נתמך בכל הדפדפנים המודרניים (2023+)

```css
/* div that contains img */
div:has(img) { padding: 20px; }

/* card with direct image child */
.card:has(> img) { padding-top: 0; }

/* label when checkbox is checked */
.agree:has(input:checked) + .btn { display: block; }

/* disable submit when form is invalid */
form:has(:invalid) button[type="submit"] { 
    opacity: 0.5; 
    pointer-events: none;  /* ignores clicks */
}
```

---

## :is() - קיצור סלקטורים

מאפשר לקצר סלקטורים חוזרים.

```css
/* instead of: */
header a:hover,
nav a:hover,
footer a:hover { color: red; }

/* use: */
:is(header, nav, footer) a:hover { color: red; }
```

---

## :where() - כמו :is() אבל ספציפיות 0

```css
/* same result, but specificity = 0 */
:where(header, nav, footer) a:hover { color: red; }
```

### מתי להשתמש?

| סלקטור | ספציפיות | שימוש |
|--------|----------|-------|
| `:is()` | לפי מה שבפנים | סטיילים רגילים |
| `:where()` | 0 | defaults שקל לדרוס |

---

## :empty - אלמנט ריק

```css
/* hide empty div */
div:empty { display: none; }

/* error message styling */
.error:empty { display: none; }
.error:not(:empty) { 
    padding: 10px;
    background: #fee; 
}
```
