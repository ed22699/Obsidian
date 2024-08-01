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
