#css #topic 

# Fonts
## Family Stacks
Browsers come with a few font "stacks".
An example font stack: `Arial, Helvetica, sans-serif`.
What it means is the browser will first look for `Arial` support; then `Helvetica`, and any `sans-serif` font will become the fallback.

Can use [Google Fonts](http://fonts.google.com) if you want to use a font not typically supported by browsers.

## Properties
There are a few font based properties you can set:
- `font-family`: sets family of the font as mentioned in [[#Family Stacks]]
- `font-size`: sets size of font using [[Measurement Units]]
- `line-height`: gap between lines, uses [[Measurement Units#Relative Units|Relative Units]]
	- recommended is `1.6em`
- `font-weight`: sets boldness of font
	- can use numbers directly
	- or text-based options like `bold`, `bolder`, etc
- `font-style`: font styling for `italic`, `oblique`, or `normal`
- `color`: sets font [[Colour Types|color]]