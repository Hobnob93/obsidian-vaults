#css #html 

# Positioning
Everything by default has a `position` of `static`.
Here are the possible `position` property values:
- `static`: Not affected by **tblr** `top`, `bottom`, `left`, `right` properties/values
- `relative`: **tblr** values cause element to be moved from its normal position
- `absolute`: positioned relative to parent that is positioned `relative`
- `fixed`: positioned relative to viewport
- `sticky`: positioned based on scroll position

You can use **tblr** properties to "push" the element from that position.
- `top`: moves element down
- `left`: moves element right
- `right`: moves element left
- `bottom`: moves element up

**Note**: Positioning like this not used in modern design much, as it isn't mobile friendly.

## Order
The higher the `z-index`, the "closer" to you it is.
Default is 0, and then sequential html order.
Can have negative values.