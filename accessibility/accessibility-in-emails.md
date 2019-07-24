# Accessibility in emails

This info sits alongside our general guide to writing emails at ????.

## Layout

- Rich visual emails typically use tables for layout.
- This is because email clients use old and conservative browser engines that do not cope well nor consistently with CSS-based layouts.
- Using ARIA to set `role="presentation"` on layout tables will help prevent them being seen as data tables by screen readers.

## Specify a language

- ??? Not sure if this makes a difference. Would put it in by default, but need to check if it's harmful.

## Alternative text

- Marketing emails tend to make heavy use of images.
- Alt text should be used the same as on a web site
- If the image conveys meaning, add an alt description.
- If the image is purely presentational, add an empty alt attribute to allow the screenreader to skip it.
- Never leave an image without an alt tag (empty of filled) as the assistive tech will read out the filename instead.

## Use logical source order

- Use the logical source order for the language you are writing in.
- For most western languages, English included, this is left to right and top to bottom.
- This includes the table cells and rows used for email layout.

## Use semantic content

- Pre-HTML5 elements `<p>` and `<h1>`, `<h2>`, etc are a good bet.

## Avoid HTML5 tags

- Anything that appeared in the HTML5 spec tends to get stripped by more conservative email clients.

## Link back to browser version

- Reliability of rendering in clients can be poor, so always have a public URL available that contains a version of the email.

## Resources

- [Why does email accessibility matter?](https://content.myemma.com/blog/why-does-email-accessibility-matter)
- [Email Accessibility: Looks aren’t everything](https://explore.reallygoodemails.com/email-accessibility-looks-arent-everything-ad0b1f6af0a4)
- [Email Accessibility Best Practices](https://www.emailonacid.com/blog/article/email-development/email-accessibilty-in-2017/)
- [Accessibility in Email Marketing | MailChimp](https://mailchimp.com/resources/accessibility-in-email-marketing/)
- [The Ultimate Guide to Accessible Emails](https://litmus.com/blog/ultimate-guide-accessible-emails)
- [Emailgeeks Slack channel](https://email.geeks.chat)
- [ZURB Foundation for Emails](https://foundation.zurb.com/emails/email-templates.html)
