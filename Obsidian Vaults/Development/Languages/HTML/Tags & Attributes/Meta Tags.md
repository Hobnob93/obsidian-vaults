#html 

# Meta Tags
Used for search engine optimisation, being discoverable online, and providing text and images previews when the site is linked to.

All meta data will use the same `<meta>` tag, the only differences being the attributes supplied in each one.

## Highly Advised Meta Data
- `<meta charset="UTF-8"/>`
  Specifies character encoding for the page.
  UTF8 is the default and is for Unicode.
- `<meta name="viewport" content="width=device-width, initial-scale=1.0">`
  Important for [[Responsive Design]]
- `<meta http-equiv="X-UA-Compatible" content="ie=edge">` 
  For browser compatibility, such as Internet Explorer.

## Search Engine Optimisation
- `<title>Your Page Title</title>` 
  Very important as it is what shows in the search engine results.
  Ensure you use the correct keywords.
- `<meta name="description" content="Some description for your page">`
  Provides some detail about the page.
  Also shows up on search engine results.
  Remember to use keywords.
- `<meta name="keywords" content="some,key,words">`
  Used to be very important but not so much in modern web SEO.
  Still fill out to contain data on what the page is about.
  Generally aim between 8-12 words.
- `<metas name="robots" content="NOINDEX, NOFOLLOW">`
  NOINDEX for if you don't want your page to be indexed by a search engine.
  NOFOLLOW if you don't want links on your page to be followed by a search engine.