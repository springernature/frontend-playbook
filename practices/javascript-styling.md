# Javascript dependent styling

A class name of `.js` on the document root element (normally `html`) is used to target JS-dependent visual styles via CSS.

## Scripts

The `.js` class must be added via a micro—but blocking—script, placed as far up in the `<head>` of the document as possible.

The blocking nature of the script prevents any visual flickering or browser reflows, unlike other techniques where JavaScript may cause styles to be applied after the page has rendered.

```html
<script>
    // JS Detection Script
    (function(e){var t=e.documentElement,n=e.implementation;t.className='js';})(document)
</script>
```

## Styles

All UI elements MUST be usable and visually-acceptable when Javascript is not present. Enhancements can be made when Javascript is present by nesting those styles underneath the `.js` class.

```scss
// Define a base style
.c-component {
	color: black;
	padding-bottom: 1rem;

}

// Add and override declarations when JS is present
.js .c-component {
	height: 200px;
	padding-bottom: 0; // overridden now that JS is present
	background-color: #e4e4e4;
	margin: 10px;
}
```
