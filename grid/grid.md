# CSS Grid

## מבוא - ההבדל בין Grid ל-Flexbox

> **Grid יוצר "מסילות" (tracks)** - שורות ועמודות שמגדירות את כל הלייאאוט מראש.
> 
> **Flexbox יוצר "גבולות לאלמנט עצמו"** - האלמנטים מתנהגים לפי התוכן שלהם ומתפרשים בציר אחד.

| Grid | Flexbox |
|------|---------|
| דו-מימדי (שורות + עמודות) | חד-מימדי (שורה או עמודה) |
| הלייאאוט נקבע על הקונטיינר | הלייאאוט נקבע לפי האלמנטים |
| מושלם לעמודים שלמים | מושלם לרכיבים קטנים |

---

## HTML בסיסי לדוגמאות

```html
<main>
    <section class="box box1">s1</section>
    <section class="box box2">s2</section>
    <section class="box box3">s3</section>
    <section class="box box4">s4</section>
    <section class="box box5">s5</section>
    <section class="box box6">s6</section>
    <section class="box box7">s7</section>
    <section class="box box8">s8</section>
</main>
```

---

## 1. grid-template-columns & grid-template-rows

מגדיר את המסילות (tracks) של הגריד - כמה עמודות/שורות ובאיזה גודל.

```css
main {
    display: grid;
    /* 3 עמודות שוות */
    grid-template-columns: 1fr 1fr 1fr;
    /* או בקיצור: */
    grid-template-columns: repeat(3, 1fr);
    
    /* 3 שורות שוות */
    grid-template-rows: repeat(3, 1fr);
}
```

### ערכים אפשריים:
- **`fr`** - Fraction unit, חלק יחסי מהמקום הפנוי
- **`px`, `%`, `em`** - יחידות קבועות
- **`auto`** - מתאים לתוכן
- **`repeat(n, size)`** - חזרה על גודל n פעמים

```css
/* דוגמה משולבת */
grid-template-columns: 200px 1fr 2fr;
/* עמודה ראשונה 200px, השנייה חלק אחד, השלישית כפול מהשנייה */
```

---

## 2. minmax()

מגדיר גודל מינימלי ומקסימלי למסילה - חיוני לרספונסיביות!

```css
main {
    display: grid;
    grid-template-columns: minmax(300px, 1fr) minmax(0, 1fr) minmax(300px, 1fr);
    grid-template-rows: minmax(300px, 1fr) minmax(200px, 1fr) minmax(300px, 1fr);
}
```

### שילוב עם auto-fit / auto-fill

```css
/* גריד רספונסיבי אוטומטי - עמודות יורדות לשורה הבאה כשאין מקום */
grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
```

| auto-fit | auto-fill |
|----------|-----------|
| מכווץ עמודות ריקות | משאיר מקום לעמודות ריקות |
| מתאים כשרוצים שאלמנטים יתפרשו | מתאים כשרוצים מבנה קבוע |

---

## 3. place-items & place-content

### place-items (מיקום האלמנטים בתוך התאים)

```css
main {
    display: grid;
    /* align-items / justify-items */
    place-items: center; /* ממרכז את כל האלמנטים בתאים שלהם */
    
    /* או בנפרד: */
    align-items: center;    /* ציר Y */
    justify-items: center;  /* ציר X */
}
```

**ערכים:** `start` | `end` | `center` | `stretch` (ברירת מחדל)

### place-content (מיקום הגריד כולו בקונטיינר)

```css
main {
    display: grid;
    height: 100vh;
    /* align-content / justify-content */
    place-content: center; /* ממרכז את כל הגריד */
}
```

**ערכים:** `start` | `end` | `center` | `stretch` | `space-between` | `space-around` | `space-evenly`

### justify-self & align-self (לאלמנט בודד)

```css
.box1 {
    justify-self: center; /* ציר X */
    align-self: center;   /* ציר Y */
    /* או: */
    place-self: center;   /* שניהם */
}
```

---

## 4. grid-column-start & grid-column-end

מגדיר מאיפה לאיפה אלמנט משתרע - לפי קווי הגריד (grid lines).

```css
.box1 {
    grid-column-start: 2; /* מתחיל מקו 2 */
    grid-column-end: 4;   /* נגמר בקו 4 (לא כולל) */
    /* = תופס עמודות 2 ו-3 */
}

.box2 {
    grid-row-start: 1;
    grid-row-end: 3;
    /* = תופס שורות 1 ו-2 */
}
```

> 💡 **קווי גריד מתחילים מ-1**, לא מ-0!

---

## 5. grid-column & grid-row (קיצור)

```css
.box1 {
    /* grid-column: start / end */
    grid-column: 2 / 4;
    grid-row: 1 / 3;
}

/* span - להתפרש על מספר תאים */
.box2 {
    grid-column: 1 / span 2; /* מתחיל מ-1, תופס 2 עמודות */
    grid-row: span 3;        /* תופס 3 שורות מהמיקום הנוכחי */
}

/* ערכים מיוחדים */
.box3 {
    grid-column: 1 / -1; /* מקצה לקצה (קו ראשון עד אחרון) */
}
```

---

## 6. grid-template-areas

דרך ויזואלית להגדיר לייאאוט - נותנים שמות לאזורים!

```css
main {
    display: grid;
    grid-template-columns: 200px 1fr 200px;
    grid-template-rows: auto 1fr auto;
    grid-template-areas:
        "header header header"
        "sidebar content aside"
        "footer footer footer";
}

header { grid-area: header; }
nav    { grid-area: sidebar; }
main   { grid-area: content; }
aside  { grid-area: aside; }
footer { grid-area: footer; }
```

### תא ריק

```css
grid-template-areas:
    "header header ."      /* נקודה = תא ריק */
    "sidebar content aside"
    "footer footer footer";
```

---

## 7. gap

רווח בין התאים (לא בקצוות!).

```css
main {
    display: grid;
    gap: 20px;              /* רווח שווה לכל הכיוונים */
    
    /* או בנפרד: */
    row-gap: 20px;          /* רווח בין שורות */
    column-gap: 10px;       /* רווח בין עמודות */
    
    /* או בקיצור: row / column */
    gap: 20px 10px;
}
```

---

## 8. grid-auto-rows & grid-auto-columns

מגדיר גודל לשורות/עמודות שנוצרות **אוטומטית** (implicit grid).

```css
main {
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    /* רק הגדרנו 3 עמודות, לא שורות */
    
    /* כל שורה שתיווצר אוטומטית תהיה לפחות 100px */
    grid-auto-rows: minmax(100px, auto);
}
```

---

## דוגמה מלאה

```css
main {
    display: grid;
    gap: 10px;
    grid-template-columns: repeat(3, 1fr);
    grid-template-rows: repeat(3, 1fr);
}

.box {
    justify-self: center;
    align-self: center;
}

.box1 {
    grid-column: 2 / 3;
    background-color: blue;
}

.box2 {
    grid-column: 1 / 2;
    grid-row: 1 / 2;
    background-color: red;
}

/* Colors for visualization */
.box3 { background-color: green; }
.box4 { background-color: yellow; }
.box5 { background-color: orange; }
.box6 { background-color: gray; }
.box7 { background-color: purple; }
.box8 { background-color: aqua; }
```
