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

h1 {
	display: none;
}

/* smartphones */
@media (max-width: 500px) {
	body {
		background: red;
	}

	#smartphone h1 {
		display: block;
	}
}

/* tablet */
@media (min-width: 501px) and (max-width: 768px) {
	body {
		background: blue;
	}

	#tablet h1 {
		display: block;
	}
}

/* normal */
@media (min-width: 769px) and (max-width: 1200px) {
	body {
		background: green;
	}

	#normal h1 {
		display: block;
	}
}

/* widescreen */
@media (min-width: 1201px) {
	body {
		background: black;
	}

	#widescreen h1 {
		display: block;
	}
}

/* landscaped mobile */
@media (max-height: 500px) {
	body {
		background: orange;
	}

	#landscape h1 {
		display: block;
	}
}
```

## Link Stylesheet Based on Media Query
```html
<link rel="stylesheet" href="mobile.css" media="screen and (max-width: 768px)"/>
```

## JSFiddle
Can see the above JS Fiddle [here](https://jsfiddle.net/Hobnob93/78za0cb3/2/).