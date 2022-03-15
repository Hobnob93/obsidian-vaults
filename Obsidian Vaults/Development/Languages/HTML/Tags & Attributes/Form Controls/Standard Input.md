#html #css

# Standard Input Field
The `<input/>` control allows for input from the user into a text box.
- `type` attribute defaults to `text`, but there are a few types:
	  - `text` - any alphanumeric data
	  - `email` - content has to be a valid email address at the point of submission
	  - `number` - only allows for numeric data entry, and it will have an incrementor control on the right side (see [[#Remove Number Increment Decrement Control|below]] on how to disable it)
	  - `date` - forces the format to be in the browser's language setting, as well as providing a simple-styled date picker
	  - `radio` - sets the input type to be a radio button (see [[Radio Buttons]])
	  - `checkbox` - sets the input type to be a checkbox (see [[Checkbox]])
	  - `submit` - create a form submission button (see [[Submit Button]])
- `name` attribute which sets the "ID" of the content when submitting the data to the server., and is how the recipient will see the data named
- `value` attribute allows for a pre-set value for the input box
- `placeholder` attribute sets a placeholder text that only shows when text box is empty, and is automatically removed when the user clicks on the control

### Remove Number Increment/Decrement Control
For the `number` type, you can **remove** the incrementor arrows by using the following CSS:
```css
input[type='number'] {
    -moz-appearance:textfield;
}

input::-webkit-outer-spin-button,
input::-webkit-inner-spin-button {
    -webkit-appearance: none;
}
```