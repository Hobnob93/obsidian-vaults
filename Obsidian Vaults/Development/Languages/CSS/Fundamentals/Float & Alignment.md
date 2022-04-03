#css #topic 

# Float & Alignment
## Containers
If you want to centre elements, use margin `auto` to equalise the margins on all sides.

Use `max-width` instead of `width` in places where you want to account for different screen dimensions.

Common to use above for containers:
```css
.container {
	max-width: 960px;
	margin: 30px auto;
}
```

## Text Aligning
By default, all `text-align` is set to `left`.
Options are:
- `left`
- `right`
- `center`
- `justify`

## Floating
More "old-school" - better to use CSS [[Grid]] or [[Flexbox]] where sensible.
Pain to use and deal with responsive design.
Useful to know them, just in case.

Use the `float` property to cause elements to be "pushed" to a side.
Options are:
- `left`
- `right`

Any elements after a floated element will render *in the same space*, which is undesired in most cases.
Fix this by adjusting the `clear` property - useful to create a "utility" class like so:
```css
.clr {
	clear: both;
}
```
Use a `div` separating the floated elements from the non-floated with class `clr` set.