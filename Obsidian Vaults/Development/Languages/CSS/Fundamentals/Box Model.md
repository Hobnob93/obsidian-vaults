#css #topic 

# Box Model
There are 4 parts to the box model, as shown in this diagram
![[Box Model Diagram.png]]

The browsers have some default spacing within the margin and borders.
This can be overridden using the [[Reset Rule]].

## Content/Element Itself
Has a width and height.
Set using the `width` and `height` properties.

## Padding
*Inside* of the [[#Border|border]].

Properties for adjusting padding:
- `padding`: sets padding for all sides in order; `top, right, bottom, left` OR `top/bottom, left/right`
- `padding-left`
- `padding-right`
- `padding-top`
- `padding-bottom`

Can set to `auto` for the same amount of padding either side.

Setting the padding changes the dimensions of the content area *unless* the `box-sizing` property is set to `border-box`.

## Border
Can set the values using [[Backgrounds & Borders#Border Properties|border properties]].

## Margin
*Outside* of the [[#Border|border]].
Increases the spacing between elements.

Properties for adjusting margin:
- `margin`: sets margin for all sides in order; `top, right, bottom, left` OR `top/bottom, left/right`
- `margin-left`
- `margin-right`
- `margin-top`
- `margin-bottom`

Can set to `auto` for the same amount of margin either side.