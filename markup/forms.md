# Form checklist

This document is to help you in the process of building forms.

## Basics

As with everything else, forms should be developed in a progressively enhanced manner. Use the SN Cutting the Mustard technique to send a Core experience to all browsers, and upgrade it to an Advanced experience when the browser is capable.

### Core experience

- Build the form with server-side generated HTML and Core CSS.
- Ensure the form can send data to a POST endpoint on the server (as specified in the form's `action` attribute), and that the server can return back to the browser either:
  - a) A success page if there are no validation errors; or
  - b) The same form with inline errors highlighted.

### Advanced experience

- Enhance the form using client-side JavaScript, so that errors and validation are checked in the browser before POSTing to the server.
- Consider creating a more inline experience by using JavaScript to send the POST data, overriding the `action` using `fetch` or `xmlhttprequest`.

## Checklist

### Buttons rather than inputs

- Specify the required attributes (name and value)

### Multistep forms over multiple submit buttons

### Server-side Validation

- Start with server-side validation
- Return an error message for each erroring form element.

### Client-side validation

### Accessibility

### Label every input

### Use the most simple form control that does the job

### Minimise the number of fields to fill out

### Mark optional fields

### Size according to the expected input

### Retain focus for every input element

- For preference, enhance it! Make it part of the brand!

### Don't ask users to repeat their email address

### Provide a "show password" option

### Don't split data fields

### Avoid dropdown menus

### Provide examples of input

- Don't use placeholders!

### Offer help text

### Masked input

### Use appropriate input types

### Explain clearly why you need any private information

### Use autocomplete when useful

### Enable auto-filling of personal details

### Use fieldsets and legends

### Make use of native validation, enhance when necessary

### Avoid native datepickers

- Controversial.
- Often better to stick with date fields.

## Resources

- https://www.smashingmagazine.com/2018/08/best-practices-for-mobile-form-design/
- https://github.com/cferdinandi/bouncer
- https://developer.mozilla.org/en-US/docs/Web/Accessibility/ARIA/forms/Basic_form_hints
