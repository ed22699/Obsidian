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