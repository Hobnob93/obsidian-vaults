#css #responsive-design #stub #topic 

# Media Queries
Can use media queries to do different styling based on the query.
```html
<div id="widescreen">
	<h1>Widescreen</h1>
</div>
<div id="normal">
	<h1>Normal</h1>
</div>
<div id="tablet">
	<h1>Tablet</h1>
</div>
<div id="smartphone">
	<h1>Smartphone</h1>
</div>
<div id="landscape">
	<h1>Landscape</h1>
</div>
```
```css
body {
	font-family: Artial, Helvetica, sans-serif;
	background: gray;
	color: white;
	text-align: center;
	padding-top: 100px;
}

@media(max-width: 500px) {
	
}
```

## JSFiddle
Can see the above JS Fiddle [here](https://jsfiddle.net/Hobnob93/rm2nkeup/3).