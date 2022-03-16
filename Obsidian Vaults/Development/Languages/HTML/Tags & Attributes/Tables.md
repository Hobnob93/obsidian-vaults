#html  #topic 

# Tables
Used for tabular data.
Used to be used for grid-like styling of websites before CSS was properly mainstream or even introduced.

## Table Tag
Defined by using the `<table></table>` tag and can contain:
- `<thead></thead>` - for displaying the header of the columns
- `<tbody></tbody>` - for the individual rows within the table
- `<tfoot></tfoot>` - for some additional data per column, such as summing of data

## Table Row Tags
A row of data is defined by using the `<tr></tr>` tag. Depending on whether it is in the header, body, or footer you'll need to use a specific tag per column contained within the `tr`:
- `<th></th>` - per column for the `thead`
- `<td></td>` - per column for the `tbody` or `tfoot`
A row has the optional attribute `span` which determines how many columns the content should span through. Through CSS, one can also set the desired column width!

## Column Group Tags
If you want to, you can set the span on width per column for the entire table in a neat way using the `colgroup` tag. See below for an example, although **note** that you *should* use CSS instead of hardcoding the style. This is just for example sake:
```html
<table>
	<colgroup>
		<col span="1" style="width: 15%"/>
		<col span="1" style="width: 60%"/>
		<col span="1" style="width: 25%"/>
	</colgroup>

	<!-- Follow up with <thead>, <tbody>, <tfoot> as normal -->
</table>
```