#css #topic 

# Visibility
## Display None
Removes the element from the browser completely; including the space it takes up.
```css
.box {
	display: none;
}
```
Useful responsive designs where you don't want some elements to show on certain screen sizes.

## Visibility Property
Same as display-none, but the element still takes up space within the window.
Simply stops the element rendering but the space remains reserved.
```css
.box {
	visibility: hidden;
}
```