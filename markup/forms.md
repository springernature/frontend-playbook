# Form checklist

This document is to help you in the process of building forms.

## Basics

For all public-facing websites, forms should be developed in a progressively enhanced manner. Use the SN Cutting the Mustard technique to send a Core experience to all browsers, and upgrade it to an Advanced experience when the browser is capable.

### Core experience

- Build the form with server-side generated HTML and Core CSS.
- Ensure the form can send data to an endpoint on the server (as specified in the form's `action` attribute), via GET or POST, and that the server can return back to the browser either:
  - a) A success page if there are no validation errors; or
  - b) The same form with inline errors highlighted.

### Advanced experience

- Enhance the form using client-side JavaScript, so that errors and validation are checked in the browser before POSTing to the server.
- Consider creating a more inline experience by using JavaScript to send the POST data, overriding the `action` using `fetch` or `xmlhttprequest`.

## Checklist

### Use appropriate input types

- Modern browsers support a variety of input types for text-like fields: 
  - `<input type='text'>`, `<input type='email'>`, `<input type='date'>`.
- Use the appropriate type for the data being requested from the user.
- Many input types will provide a more appropriate keyboard interface to the user.

### Buttons rather than inputs

- Specify the required attributes (name and value)
- Buttons allow inline elements to be placed inside them (e.g. spans, SVGs, and images)
- Specify `type='submit'` for the main form submit button.
- All buttons not for submitting form data to a server should have their `type` attribute set to `button`. Otherwise they will by default try to submit form data.

### Multistep forms over reactive forms

- We build robust sites that do not rely on client-side JS.
- Form-based products should be designed from the start with form submission in mind.
- An interactive form design would need research to show why it is necessary over a robust multi-step form.
  - Any user-critical interactive form would still need to be made progressively enhanced, meaning more work.
- As well as being more robust, a simple multi-step brings the additional benefit of being more usable and accessible, and, if GET query strings are exposed, shareable at every step.

### Ensure server-side validation occurs

- Part of the Core experience, so every form should be initially built to the Core standards.
  - Data should be validated on the server, and a form with inline messages for any errors encountered.
- All data being sent to a server must be sanitised, so server-side validation is always necessary.

### Allow client-side validation to occur

- Client-side validation is a supplement to server-side validation, not a replacement.
- Part of the Advanced experience.
- Validate form fields using HTML5 native browser capabilities whenever possible.
  - This allows client-side validation to occur in Advanced browsers where JS has failed.
- Augment native browser validation with JavaScript.
  - [Bouncer JS](https://github.com/cferdinandi/bouncer), for example, is designed to enhance native browser validation.

### Label every input

- Every input must have a corresponding label.
- We prefer separate labels linked via a `for` attribute, rather than labels that wrap around the input.
- Separate labels are generally easier to style.

We do NOT do this:

```html
  <label>
    Label text
    <input type="text">
  </label>
```

We do this:

```html
<label for="myinput">Label text</label>
<input type="text" id="myinput">
```

### Be generous with help text

- Provide as much help text as necessary for the user to succeed at their task. Don't hold back information for aesthetic reasons!

### Avoid `<select>` when possible

- `<select>` menus have accessibility and usability considerations.
- Replace `<select>` with `<input type='radio'>` whenever possible.
- If you have too many options for radio buttons, then consider how you could better present the data.

### Mark optional fields

- Highlight form fields that are _optional_, rather than highlighting fields that are required.
- Consider removing optional form fields: if they are optional then why is the data being collected?
- Fewer fields means less cognitive work for the user!

### Minimise the number of fields to fill out



### Size according to the expected input

- Form inputs should accommodate the expected input.
- If the expected input is highly variable, size for a median value.

### Retain focus for every input element

- Removing focus is a huge accessibility fail.
- Rather than being removed, the focus should be incorporated into the design of the page.

### Don't ask users to repeat their email address

- Asking a user to repeat their email address introduces barriers to them using the form.
- If an email address is critical for a system then confirm it by sending a confirmation link to that address.

### Provide a "show password" option

- As with emails, do not ask users to repeat their password.
- Provide a JavaScript reveal option to let users view the password that they have typed.

### Don't split data fields

### Masked input

### Avoid dropdown menus

### Provide examples of input

- Don't use placeholders!

### Offer help text



### Explain clearly why you need any private information

### Use autocomplete when useful

### Enable auto-filling of personal details

### Use fieldsets and legends

### Make use of native validation, enhance when necessary

### Avoid native datepickers

- Controversial.
- Often better to stick with input fields.

### Consider how your form interacts with autofill

## Resources

- https://www.smashingmagazine.com/2018/08/best-practices-for-mobile-form-design/
- https://github.com/cferdinandi/bouncer
- https://developer.mozilla.org/en-US/docs/Web/Accessibility/ARIA/forms/Basic_form_hints
