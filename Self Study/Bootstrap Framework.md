pre-made css files. Include bootstrap.css
```html
<head>
   <link href="link for bootstrap CDN">
</head>
<body>
   <ul class="nav nav-pills">
        <li>
           <button class="nav-link active rounded-5">Home</button>
        </li>
     </ul>
</body>
```
Pros:
- easy and fast
- good browser compatibility

Cons:
- class blur, lots of css in the html
- cannot customise

- use when you making a quick responsive mobile first design
- not for simple or complex custom websites

Use through CDN (Content delivery network)
include link in the head section and the script just before the end of the body section

## Bootstrap layout
bootstrap container changes automatically for different sized screens
- container is split into 12 pieces, size columns like so
```html
<div class="container">
   <div class="row">
      <div class="col-2">hello</div>
      <div class="col-4">hello</div>
      <div class="col-6">hello</div>
   </div>
</div>
```
default break points means you can say stuff such as
- `col-sm-2` on a small screen and above give 2/12th, below it gives each div 100%
- `col-sm-12 col-md-8 col-lg-4`, this means on large screens take up 4 slots, on medium take up 8 and on small take on 12
- `col` will just take the rest of the room

## Bootstrap Components
add in the script link file to add functionality