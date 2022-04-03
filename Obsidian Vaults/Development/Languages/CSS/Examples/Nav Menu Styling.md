#css #html #jsfiddle 

# Nav Menu Styling
Usually created using the `ul` element.
Lists usually come with bulleted styling by default; can remove these with the `list-style` property, setting it to `none`;
They also have large padding on the left side by default; this can also be changed.

Use [[Pseudo-Selectors|pseudo selectors]] for first and/or last child in the list.

## Side Menu
A simple example of a side-styled navigation menu:
```css
body {
	font-family: Arial, Helvetica, sans-serif
}

.side-menu {
	list-style: none;
	border: 1px #dddddd solid;
	border-radius: 10px;
	width: 300px;
	padding: 20px;
}

.side-menu li {
	font-size: 18px;
	line-height: 2.4em;
	border-bottom: dotted 1px #dddddd
}

.side-menu li:last-child {
	border: none;
}

.side-menu li a {
	color: #333333;
	text-decoration: none;
}

.side-menu li a:hover {
	color: coral;
}
```
```html
<body>
	<ul class="side-menu">
		<li><a href="#">Home</a></li>
		<li><a href="#">About</a></li>
		<li><a href="#">Services</a></li>
		<li><a href="#">Contact</a></li>
	</ul>
</body>
```

## Horizontal Menu
```css
body {
	font-family: Arial, Helvetica, sans-serif
}

.navbar {
	list-style: none;
	margin: 0;
	padding: 0;
	background: #4c6ca0;
	border-radius: 5px;
	overflow: auto; /* retains background when floating */
}

.navbar li {
	float: left;
}

.navbar li a {
	display: block;
	color: #ffffff;
	text-decoration: none;
	padding: 15px 20px;
}

.navbar li a:hover {
	background-color: #446190;
	color: #f4f4f4;
}
```
```html
<body>
	<ul class="navbar">
		<li><a href="#">Home</a></li>
		<li><a href="#">About</a></li>
		<li><a href="#">Services</a></li>
		<li><a href="#">Contact</a></li>
	</ul>
</body>
```

## JSFiddle
Can see the [[#Side Menu]] JSFiddle [here](https://jsfiddle.net/Hobnob93/95nabd8y/2)
Can see the [[#Horizontal Menu]] JSFiddle [here](https://jsfiddle.net/Hobnob93/q1jou5yp/)