#html #css 

# Text Area Input Field
There is a `<textarea/>` control which is like the standard `input` but offers multiple lines of input data - generally used for bigger chunks of input string.
- `name` attribute performs the same purpose as the standard `input` control
- `cols` attribute increases the width of the control
- `rows` attribute increases the height of the control

The control has a draggable grip on the bottom right so the user can increase/decrease the size. To **disable** this, you can change the `resize` property in CSS:
```css
textarea {
	resize: none;
}
```