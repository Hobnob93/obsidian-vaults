#css #topic 

# Specificity
Determines the overall styling of an element based on how "specific" the targeting styles are. See below for a general example.

Using the code below, the first `h1` will be blue, but the second will be red.
```css
h1 {
	color: blue;
}

.red {
	color: red;
}
```
```html
<h1>I am blue!</h1>
<h1 class="red">I am red!</h1>
```

## Overriding Specificity
Can do this by using the `!important` flag - this will override specificity, unless something with a higher specificity is also marked as important.