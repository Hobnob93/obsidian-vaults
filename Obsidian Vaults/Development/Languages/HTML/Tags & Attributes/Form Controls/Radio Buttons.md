#html 

# Radio Buttons
It uses the [[Standard Input]] tag with the `type` attribute set to `radio`. The `value` attribute contains the data that is sent to the backend if the button is checked.

If there are multiple radio buttons grouped together, they all need to contain the same `name` attribute. A grouping of radio buttons can only have **one** option checked at a time.

You can set the `checked` attribute to have a button selected by default.

The "label" for each radio button can be inserted immediately after the `input` tag as raw text.

See below an example of a membership selection radio button group:
```html
<div>
	<label for="membership">Membership</label><br/>
	<input type="radio" name="membership" value="simple"> Simple
	<input type="radio" name="membership" value="standard" checked> Standard
	<input type="radio" name="membership" value="premium"> Premium
</div>
```