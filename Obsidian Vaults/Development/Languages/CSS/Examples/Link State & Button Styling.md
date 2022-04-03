#css #html #jsfiddle 

# Link State & Button Styling
## Links
Links are often set using the anchor `<a></a>` tag.
Links by default are underlined; you can remove this by changing the `text-decoration` property to `none`.

You can use a [[Pseudo-Selectors|pseudo selector]] to change the `hover` styling, such as the text colour:
```css
a:hover {
	color: coral;
}
```

Can adjust the styling if the link has been visited using another [[Pseudo-Selectors|pseudo selector]]:
```css
a:visited {
	color: aliceblue;
}
```

Set the active state (when user clicks/"selects" it):
```css
a:active {
	color: red;
}
```

## Buttons
Common to create a `.btn` class, and then light and dark options such as `btn-light` and `btn-dark`.
Can then use the `.btn` class on both anchors AND button elements to make them look the same.

Example of making a `.btn` class and setting font:
```css
body {
	font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif
}

.btn {
	background: #4c6ca0;
	color: #ffffff;
	border: none;
	font-size: 16px;
	padding: 10px 20px;
	border-radius: 5px;
	cursor: pointer;
	text-decoration: none;
}

.btn:hover {
	color: #f4f4f4;
	background: #446190;
}
```
```html
<body>
	<br>
	<a class="btn" href="#">My Link</a>
	<br>
	<br>
	<button class="btn">My Button</button>
</body>
```

## JSFiddle
Can see the [[#Buttons]] JS Fiddle [here](https://jsfiddle.net/Hobnob93/rm2nkeup/3).