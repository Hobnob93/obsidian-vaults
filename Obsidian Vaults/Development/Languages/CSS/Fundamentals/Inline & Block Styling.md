#css #topic #html 

# Inline & Block
The ability to change whether elements are inline or block, as per [[Block & Inline Level Elements]].
This can be changed using the `display` property.

## Changing Block to Inline
The example below makes a horizontal menu by changing `ul` `li` elements to *not* be block.
```css
li {
	display: inline;
}

li a {
	padding-right: 20px;
}
```
```html
<body>
	<ul>
		<li><a href="#">Technology</a></li>
		<li><a href="#">Business</a></li>
		<li><a href="#">Fashion</a></li>
	</ul>
</body>
```

## Changing Inline to Block
Sometimes want to do this with `image` tag.
Might want to do this to ensure images are in the middle and not have other images to the side of it.
While it is *inline*, setting `margin: auto` **will not work**.
```css
img {
	display: block;
	margin: auto;
}
```
```html
<body>
	<img src="./img/leaf.png" />
</body>
```

## Using Inline-Block
Suppose the following CSS:
```css
.box {
	width: 32%;
	display: inline;
	box-sizing: border-box;
	background: #f4f4f4;
	padding: 20px;
	margin-bottom: 15px;
}
```
This *will not work* as expected.
Properties `width` and `margin` cannot be set when `display: inline`.
Solution is to use `inline-block`.