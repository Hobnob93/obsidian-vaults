#best-practise #css #topic

# Reset Rule
A good practise when creating CSS from scratch is to implement a CSS reset.

It essentially removes all default styling, and sets it to something you specify.

## Specify a Custom Reset Style
You can use the following as a go-to reset style:
```css
* {
	margin: 0;
	padding: 0;
	border: 0;
	box-sizing: border-box;
}
```

Just make sure to define this style *before* all other styles!

## Recommendation
It is advised to create a `css` file *just* for the reset class, and then `link` it *before* all the other css files that are to be linked.