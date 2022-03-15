#html 

# Checkbox
It uses the [[Standard Input]] tag with the `type` attribute set to `checkbox`. The `value` attribute contains the data that is sent to the backend if the box is checked.

If there are multiple checkboxes buttons grouped together, they all need to contain the same `name` attribute. A grouping of checkboxes have **any number** of options checked at a time.

You can set the `checked` attribute to have a button selected by default.

The "label" for each checkbox can be inserted immediately after the `input` tag as raw text.

See below an example of an opinion pole with C# checked by default:
```html
<div>
	<label for="membership">I like the following languages</label><br/>
	<input type="checkbox" name="liked-language" value="cs" checked> C#
	<input type="checkbox" name="liked-language" value="cpp"> C++
	<input type="checkbox" name="liked-language" value="c"> C
	<input type="checkbox" name="liked-language" value="js"> JavaScript
</div>
```