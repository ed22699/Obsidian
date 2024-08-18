2D layout
```html
<div class="container">
   <p>...</p>
   <p>...</p>
   <p>...</p>
   <p>...</p>
</div>
```
```css
.container {
   display: grid;
   grid-template-columns: 1fr 2fr;
   grid-template-rows: 1fr 1fr;
   gap: 10px;
}
```
![[Excalidraw/css grid|css grid]]
## Grid Sizing
- fixed size `100px` will not be responsive
- relative size `1rem` will not be responsive
- `auto` each row tries to fit to 100% of available space (tries to fit to content when applied to rows) is responsive
- `1fr` splits into ratios, is responsive
- `grid-template: 1fr 2fr / 1fr 1fr` is the same as what is written above (combines columns and rows into 1)
### Min-max
```css
.container {
   display: grid;
   grid-template-rows: 200px 400px;
   grid-template-columns: 200px minmax(400px, 800px)
}
```
- when enough space second column goes all the way up to `800px`
- can shrink second column to `400px`
- `1fr 1fr 1fr` is equal to `repeat(3, 1fr)`
- `grid-auto-rows` if items overflow grid definition it will size these new items with the grid-auto definitions

## Grid Placing
![[grid placement]]
```html
<div class="container">
   <div class="item green"></div>
   <div class="item red"></div>
   <div class="item blue"></div>
```
```css
.container {
   height: 100vh;
   display: grid;
   gap: 3rem;
   grid-template-columns: 1fr 1fr 1.5fr;
   grid-template-rows: 1fr 1fr;
}

.item{
/* flex box is useful for centering items within layouts */
   display:flex;
   justify-content: center;
   align-items: center;
}

.green{
   background-color: green;
   grid-column: span 2;
}

.red{
   background-color: red;
   grid-column-start: 2;
   grid-column-end: 4;
   /* or use
   grid-column-end: -1 */
   order: 1;
}

.blue{
   background-color: blue;
   grid-row: span 2;
}
```
- grid lines is defined using `gap`
- tracks are defined with `grid-template-columns` and `grid-template-rows`
- `grid-area: 2 / 1 / 3 / 2` goes in the order grid-row-start, grid-column-start, grid-row-end, grid-column-end
- you can also overlap items with grid-area