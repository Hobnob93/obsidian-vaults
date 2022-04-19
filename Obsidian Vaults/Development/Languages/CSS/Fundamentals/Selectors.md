#css #topic

# Selectors
## Selecting by element type
We can target an element type, such as an `<h2>`:
```css
h2 {
	color: green;
}
```

## Selecting by element ID
We can target a specific element directly, through its html ID:
```css
#green-element {
	color: green;
}
```

## Selecting by element class
We can target any number of elements that sign up to a particular `class`
```css
.primary-heading {
	color: blue;
}
```

## You can combine multiple selectors
Can be any combination of the above selectors:
```css
.class-1, #id1 {
	background-color: red;
}
```

## Targeting nested elements
A space indicates a child:
```css
.parent-class .child-class {
	font-size: 20px;
}
```

## Order of Precedence
[[Specificity]] defines the order of precedence that will ultimately decide how an element gets styled.
Can affect the order by using the `!important` flag - this will override specificity, unless something with a higher specificity is also marked as important.