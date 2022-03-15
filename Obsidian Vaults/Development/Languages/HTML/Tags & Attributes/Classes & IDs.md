#html 

# Classes & IDs
In terms of CSS, they have very similar behaviours. You're able to use them in selectors and create styles for elements with these classes or IDs.

Use classes for when you want a re-usable style which multiple elements will implement.

Use IDs when you want a style applied to just a single element, as IDs should be unique on a given page.

IDs and Classes have additional usage when it comes to JavaScript, as we can fetch elements from the [[DOM]] (libraries like [[jQuery]] make this easier). When fetching, we can select a group of elements using a `class` (or some other non-unique selector); or we can select a single element directly using the `id`.