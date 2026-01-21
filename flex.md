# Flexbox – One Demo + Line-by-line

## HTML
```html
<main class="container">
  <section class="box a">A</section>  
  <section class="box b">B</section>  
  <section class="box c">C</section>  
</main>


.container {
  display: flex;                 /* Enables Flexbox for the direct children */
  flex-direction: row-reverse;   /* Sets the main axis direction to a reversed row */
  flex-wrap: nowrap;             /* Prevents items from wrapping to a new line */
  flex-flow: row-reverse nowrap; /* Shorthand for direction + wrap (overrides the two lines above if both exist) */
  justify-content: flex-start;   /* Positions items at the start of the main axis */
  align-items: stretch;          /* Stretches items along the cross axis */
  gap: 2px;                      /* Adds spacing between items */
}

.box {
  flex-grow: 1;                  /* Allows the item to grow when there is free space */
  flex-shrink: 1;                /* Allows the item to shrink when there is not enough space */
  flex-basis: 200px;             /* Sets the initial size used for flex calculations */
  flex: 1 1 200px;               /* Shorthand for grow/shrink/basis (must use spaces, not commas) */
  align-self: stretch;           /* Overrides cross-axis alignment for this item if needed */
}

.b {
  order: 1;                      /* Changes visual order (does not change the DOM order) */
}
