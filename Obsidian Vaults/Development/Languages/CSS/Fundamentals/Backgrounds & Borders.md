#css #topic 

# Backgrounds & Borders
## Border Properties
- `border-width`: ==mandatory== border property - set width using any [[Measurement Units|units]]
- `border-color`: ==mandatory== border property - sets border [[Colour Types|colour]]
- `border-style`: ==mandatory== for type of "line" to use as the border, common options are:
	- `dashed`
	- `groove`
	- `dotted`
	- `double`
	- `solid`

Can merge all border properties into one property:
```css
h1 {
	border: 3px solid red;
}
```

Have a border on a specific side using:
- `border-left`
- `border-right`
- `border-top`
- `border-bottom`

Rounded corners
- `border-radius`: provide a [[Measurement Units|unit]] of your choice
- `border-top-left-radius`: will only round the top left border

## Background Properties
- `background`: lets you set a [[Colour Types|colour]]
- `background-image`: use the `url()` function to point to an image for background
- `background-repeat`: repeats an image - best used with seamless images
	- option to `repeat-x` or `repeat-y`
- `background-position`: moves the image around within its container
	- takes `x` and `y` axis
	- can use `center`, `left`, `right`, `top`, or `bottom` to position on `x` and/or `y`