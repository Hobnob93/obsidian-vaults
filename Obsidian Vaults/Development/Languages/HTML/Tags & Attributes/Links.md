#html #topic 

# Links
These are represented with an `<a href=""></a>` tag, with a *required* `href` attribute - containing the endpoint of where you want the link to navigate.

The inner html contains the text you want to be displayed as the anchor.

This will open in the *same* tab by default - to change this add the `target="_blank"` attribute.

Anchor tags are an *inline* element (see [[Block & Inline Level Elements]]) so multiple next to each other will appear on the same line by default.

You can have both *internal* and *external* links. See below.
```html
<!-- Internal Link -->
<a href="/some-local-file.html">Click for Internal</a>

<!-- External Link -->
<a href="http://google.com">Click for Google</a>
```