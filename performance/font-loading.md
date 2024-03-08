# Font loading

- [When to use webfonts](#when-to-use-webfonts)
- [Implementation](#implementation)
- [Quick tips](#quick-tips)
  - [Understand the different user experiences in font loading: FOIT, FOUT and FOFT](#understand-the-different-user-experiences-in-font-loading-foit-fout-and-foft)
  - [Understand the different implementations available](#understand-the-different-implementations-available)
  - [WOFF and WOFF2 font formats](#woff-and-woff2-font-formats)
  - [font-display CSS](#font-display-css)
  - [Loading fonts with JavaScript](#loading-fonts-with-javascript)
  - [Preloading webfonts](#preloading-webfonts)
  - [Self host webfonts if possible](#self-host-webfonts-if-possible)

## When to use webfonts

Webfonts allow us to bring emotion, personality and tone to our sites - which can make them more successful.

However, the task of choosing a webfont and implementing it on your site should be approached cautiously. Webfonts have the potential to impact aspects of your sites such as accessibility and page speed. For example:

- Certain webfonts may reduce the readability of the site, for example for people with dyslexia, or low vision.
- Webfonts can negatively impact page performance (additional http requests and increased page weight) especially in markets of strategic importance for Springer Nature like China. This will in turn impact usage numbers.

Our recommendation is that you prioritise a [system font](https://css-tricks.com/snippets/css/system-font-stack/) over a webfont. System fonts are extensively tested, and incur no performance penalty.

If a webfont is needed then close collaboration between user experience, accessibility, and web performance specialists must be sought to ensure the choice is satisfactory from typographic, accessibility, and performance perspectives.

As a Frontend Developer, it's your role to provide technical guidance and feedback, not to choose the font.

## Implementation

We do not prescribe a particular implementation. Each team should determine which implementation is best suited for them. However, before selecting an implementation a team should be mindful of our working practices such as:

- [Graded Browser Support](https://github.com/springernature/frontend-playbook/blob/main/practices/graded-browser-support.md)
  - Is the implementation supported by all "enhanced" browsers? If not, is there a good justification for selecting it anyway?
  - Does the implementation work in conjunction with the Cut The Mustard technique?
- [Progressive Enhancement](https://github.com/springernature/frontend-playbook/blob/main/practices/progressive-enhancement.md)
  - This is not meant to force you to choose a non-js implementation, but rather for you to ensure you consider what will happen for users in varying circumstances from the beginning.
- [Our Performance Goals](https://github.com/springernature/frontend-playbook/blob/main/performance/performance-checklist.md)
  - What impact will the implementation have on the page performance of your site?

## Quick tips

Here are some quick suggestions for techniques that may prove useful:

### Understand the different user experiences in font loading: FOIT, FOUT and FOFT

- FOIT means _flash of invisible text_. Text on the page is hidden while webfonts are loading, so users will see a page with images but no text. We only show the text when webfonts are loaded.
- FOUT means _flash of unstyled text_. When webfonts are loading, we show users a system font. When the webfont gets loaded, we change the text back to the desired webfont.
- FOFT means _flash of faux text_. Only load the roman character set initially and load the others later for less page render blocking. "Faux" refers to the fact the browser fakes italics and bold before those character sets have loaded.

We believe that FOIT should be avoided as it is the worst experience for the user.

### Understand the different implementations available

We highly recommend reading [Zach Leat's comprehensive guide](https://www.zachleat.com/web/comprehensive-webfonts/) to get a good understanding of the different techniques available. There is also a good [follow-up article](https://css-tricks.com/the-best-font-loading-strategies-and-how-to-execute-them/) that summarises Zach's findings.

### WOFF and WOFF2 font formats

WOFF2 has a superior compression, and [is supported by all of our Enhanced browsers](https://caniuse.com/woff2), so there's no need to serve fonts in WOFF format.

### [font-display CSS](https://developer.mozilla.org/en-US/docs/Web/CSS/@font-face/font-display)

[`font-display`](https://developer.mozilla.org/en-US/docs/Web/CSS/@font-face/font-display) is useful and has the benefit of being a technique that does not require JavaScript and is easy and straight forward to implement.

We recommend reading this [comprehensive analysis of font-display](https://calendar.perfplanet.com/2020/a-font-display-setting-for-slow-connections/) values when deciding which value is best for you.

### Loading fonts with JavaScript

Consider using [FontFaceObserver](https://github.com/bramstein/fontfaceobserver) instead of the [CSS Font Loader API](https://drafts.csswg.org/css-font-loading/), as the latter does not have support for all our Enhanced browsers.

### Preloading webfonts

If you have to load a font the conventional way using a `<link>` then consider using the [preload technique](https://web.dev/preload-critical-assets/) to ensure the font is requested as early on in the page load process as possible.

`<link rel="preload" href="HardingText-Regular-Web.woff2" as="font" type="font/woff2" crossorigin>`

### Self host webfonts if possible

Some webfonts prevent you from self hosting because of their licensing so check that first. But if you can, consider self hosting a font. This will potentially reduce the possible points of failure or poor page performance, and it will open up more options to you in terms of possible font loading implementations.
