# Accessibility in emails

Accessibility in emails can be summarised with 3 key points:

1. Accessible emails allow you to reach a wider audience.
1. Writing and visual design are key components of an accessible email campaign, so ensure that UX and content folk are involved in all discussions.
1. Email templates can be made immediately more accessible with a few simple coding techniques.

Creating accessible emails is not fundamentally different from creating accessible websites.

Here are the few differing constraints and techniques that should be considered.

## Layout

Rich visual emails typically use tables for layout. This is because email clients use old and conservative browser engines that do not cope well nor consistently with CSS-based layouts.

- Using ARIA to set `role="presentation"` on layout tables will help prevent them being seen as data tables by screen readers.

## Specify a language

Emails, even if sent in English, can be read out loud by browsers and operating systems using other languages.

- Setting the language of the email on the root element will allow assistive technology to use the appropriate language profile.

## Alternative text

Marketing emails tend to make heavy use of images, so it is important to ensure alt text is used well.

- Alt text should be used as it would be on a web site.
- If the image conveys meaning, add an alt description.
- If the image is purely presentational, add an empty alt attribute (`alt=""`) to allow the screenreader to skip it.
- If the image is an image of text, the alt attribute must contain that same text.
- Never leave an image without an alt attribute as the assistive tech will read out the filename instead. If you're sure the image doesn't need alt text, use an empty alt attribute (`alt=""`). 
- Do not use alt text to prompt the user to enable images in their email client.

## Use logical source order

Screenreaders will rely on the logical source order of the HTML when they read out content.

- Use the logical source order for the language you are writing in.
- For most western languages, English included, this is left to right and top to bottom.
- This includes the table cells and rows used for email layout.

## Use semantic content

Semantic HTML helps screenreaders to read out content, and allows the email to be visually interpreted even if CSS is not available.

- Pre-HTML5 elements `<p>` and `<h1>`, `<h2>`, are likely to work in all clients.

## Avoid HTML5 elements

Any HTML elements that appeared in the HTML5 specification may be stripped by more conservative email clients.

- Avoid using HTML5 elements, such as `<main>`, `<aside>`, etc.
- This differs from the accessibility advice normally given for browser markup.

## Link back to browser version

Reliability of rendering in clients can be poor.

- Always have a public URL available that displays an HTML version of the email.

## Resources

- [Why does email accessibility matter?](https://content.myemma.com/blog/why-does-email-accessibility-matter)
- [Email Accessibility: Looks aren’t everything](https://explore.reallygoodemails.com/email-accessibility-looks-arent-everything-ad0b1f6af0a4)
- [Email Accessibility Best Practices](https://www.emailonacid.com/blog/article/email-development/email-accessibilty-in-2017/)
- [Accessibility in Email Marketing | MailChimp](https://mailchimp.com/resources/accessibility-in-email-marketing/)
- [The Ultimate Guide to Accessible Emails](https://litmus.com/blog/ultimate-guide-accessible-emails)
- [Emailgeeks Slack channel](https://email.geeks.chat)
- [ZURB Foundation for Emails](https://foundation.zurb.com/emails/email-templates.html)
