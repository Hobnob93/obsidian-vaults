#html 

# Doc Type & Basic Layout
## DOCTYPE Declaration
The doc type `<!DOCTYPE>` declaration *must* be the *first* thing in the html document, before the `<html>` tag.

It is *not* an HTML syntax tag - it is purely an *instruction* to the browser to tell it what version of html the file is.

For HTML5 we want to use `<!DOCTYPE html>`.

You can see more doc types at [W3Schools](https://www.w3schools.com/tags/tag_doctype.asp).

## HTML Tag
You need to put the `<html></html>` tag immediately after the DOCTYPE declaration.

Optionally contains the `lang="en"` attribute to specify the web page language as English (can of course specify other languages).

The web page will be enclosed within this tag.

## Head Tag
Stores data about the page, such as meta. Doesn't display in the browser itself.

Uses `<head></head>`. Contains other important tags like `<title></title>`; where stylesheets are linked via the `<link/>` tag; and where [[Meta Tags]] can be included.

## Body Tag
Items to be displayed on the actual web page on the front end.

Contained within the `<body></body>` tag, which comes after the [[#Head Tag]].