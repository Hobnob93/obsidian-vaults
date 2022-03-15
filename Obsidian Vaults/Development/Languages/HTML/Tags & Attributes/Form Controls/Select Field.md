#html 

# Select Field
Also known as a Combo Box, or a Drop Down Field.

Use the `<select></select>` tag; the items that can be selected will go within the inner html.

An `<option></option>` tag is used for each individual selectable option within the drop down field. The text to be shown in the drop down is inserted into the inner html.
- `value` attribute - what the backend sees when the form is submitted
- `selected` attribute - the selected option, if not supplied it will be the first `option` within the list

Example drop down field of cars, where `Audi` is the default selected:
```css
<select id="cars">
	<option value="volvo">Volvo</option>
	<option value="saab">Saab</option>
	<option value="vw">VW</option>
	<option value="audi" selected>Audi</option>
</select>
```