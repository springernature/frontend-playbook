# Accessibility in emails

This info sits alongside our general guide to writing emails at ????.

## Layout

- Rich visual emails typically use tables for layout.
- ??? Setting `role="presentation"` seems like a good idea, but some ppl recommend against it. 

## Specify a language

- ??? Not sure if this makes a difference. Would put it in by default, but need to check if it's harmful.

## Alternative text

- Marketing emails tend to make heavy use of images.
- Alt text should be used just the same as on a web site
- If the image conveys meaning, add an alt description.
- If the image is purely presentational, add an empty alt attribute.

## Use logical source order

- Use the logical source order for the language you are writing in.
- For most western languages, English included, this is left to right and top to bottom.
- This includes the table cells and rows used for email layout.

## Use semantic content

- Pre-HTML5 elemets `<p>` and `<h1>`, `<h2>`, etc are a good bet.

## Avoid HTML5 tags

- Anything that appeared in the HTML5 spec tends to get stripped by more conservative email clients.

## Link back to browser version

- Reliability of rendering in clients can be poor, so always have a public URL available that contains a version of the email.


## Resources

- Litmus
