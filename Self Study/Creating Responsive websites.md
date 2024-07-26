---
tags:
  - CSS
---
1. [[Media Queries]] - good for resizing screens
```css
@media (max-width: 600px){
    /* CSS for screens below or equal to 600px wide */
}
```

2. CSS Grid - good for 2D layout
```css
.grid-container {
    display: grid;
    grid-template-columns: 1fr 1fr;
    grid-template-rows: 100fr 200fr 200fr;
    gap: 30px;
}
```

3. CSS Flexbox - good for 1D layout
```css
.flex-container{
   display: flex;
}
```

4. Bootstrap Framework - predefined layout