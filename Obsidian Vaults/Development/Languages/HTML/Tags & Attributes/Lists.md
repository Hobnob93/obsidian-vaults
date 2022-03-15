#html 

# Lists
## Unordered List
Intended for items in no particular order.
The html for an unordered list:
```html
<ul>
	<li>Item 1</li>
	<li>Item 2</li>
	<li>Item 3</li>
</ul>
```

The bullets will be there by default - they can be removed or changed via CSS.

Very often used for navigation menus whether horizontal menu or sidebar.

## Ordered List
Intended for items where there is an order as bullets are replaced by numbers by default.
The html for an ordered list:
```html
<ol>
	<li>Item 1</li>
	<li>Item 2</li>
	<li>Item 3</li>
</ol>
```

There is a `type` attribute that can be used. It has the following options:
- `type="1"` - will number the items; 1. 2. 3. etc.
- `type="A"` - will upper case letter the items; A. B. C. etc.
- `type="a"` - will lower case letter the items: a. b. c. etc.
- `type="I"` - will upper case roman numeral the items; I. II. III. etc.
- `type="i"` - will lower case roman numeral the items; i. ii. iii. etc.

## Nested Lists
You can contain lists within lists if you so desire (the list type can also be mixed and matched):
```html
<ol type="1">
	<li>Item 1</li>
	<li>Item 2
		<ol type="a">
			<li>Item 2.a</li>
			<li>Item 2.b</li>
			<li>Item 2.c</li>
		</ol>
	</li>
	<li>Item 2</li>
</ol>
```

The nested list will automatically change the bullet/style - so `ul` for example will use a solid circle on the outer list and a hollow circle as the bullet for the inner list.