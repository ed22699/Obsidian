don't use [[floatCSS]] for layout use flexbox instead

### HTML
```html
<div class="container">
    <div class="one"><p>...</p></div>
    <div class="two"><p>...</p></div>
    <div class="three"><p>...</p></div>
</div>
```
### CSS
```css
.containter {
    display: flex;
    gap: 10px;
}
```
note [[CSS Display]] is used, however this instance does not abide by the same rules 

- will attempt to display all in 1 line
`inline-flex` is like flex however does not have to take up the entire line

## Flex Direction
by default `flex-direction: row`
- row - from left to right
- column - from top to bottom
`flex-basis` is the width or hight depending on the direction 
>[!NOTE]
>`flex-basis` cannot be ran on the container. Need to do container > *
> (related to [[CSS selectors]])

## Flex Layout
Theres the container and the child
- you can change the `order` property, the highest order goes rightmost
- `flex-wrap` default `nowrap` keeps on one line and shrinks until it can't anymore
	- `wrap` will bring it to the next line when full
- `flex-direction` is the direction in which they are ordered. To reverse this change to `row-reverse`
- `justify-content` default `flex-start` bunches to the left
	- `flex-end` bunches to the right
	- `center` centers the properties
	- `space-between` even distribution
- `align-items` default `flex-start`, need to set the height of the container `height: 70vh;` where `vh` means view port height
- can change single child property with `align-self`
- `align content` will only work when `flex-wrap: wrap`
[A Complete Guide To Flexbox | CSS-Tricks](https://css-tricks.com/snippets/css/a-guide-to-flexbox/)
for single items use `order`, `align-self`
- `flex-flow: row wrap` is the combination of `flex-direction` and `flex-wrap`

## Flex Sizing
Content width < Width < flex-basis < min-width/max-width
- `flex-grow` if changed to 1 each item is increased in width until row is full
- `flex-shrink` if changed to 1 each item can be shrunk to its min-width
- `flex-basis` default is `auto` gives more to items with more content, if 0 it will give all equal content
- can shorthand with `flex: 0 0 0` with grow shrink basis
- `flex: 1` is the same as `flex: 1 1 0`
- you can create a ratio for elements with `flex: 1` for one element and `flex: 2` for another