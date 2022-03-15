#html 

# Submit Button
There are a few ways in which to create a submit button, which will ultimately serialise and submit the form to the backend.

## Input as Button
This approach uses the [[Standard Input]] tag with the `type` set to `submit`, and the `value` set to whatever you want the button text to be.

Example:
```html
<input type="submit" value="Submit">
```

## Button Tag
The alternative option is to use a [[Button]] tag with the `type` attribute set to `submit`.

The inner html of `button` needs to be set to the text you want displayed on the button itself.

Example:
```html
<button type="submit">Submit</button>
```