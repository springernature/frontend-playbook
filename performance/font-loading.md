# Font Loading

## When to use webfonts
Before using webfonts it's worth understanding what benefits you believe a webfont will provide your product and assess those against the potential impact they may have on things like accessibility or page speed. For example:

- System fonts are battle tested and were produced with legibility in mind. Using webfonts may reduce the readability of the site, especially for people with dyslexia.
- Webfonts can negatively impact page performance (additional http requests and increased page weight) especially in markets of strategic importance for Springer Nature like China. This will in turn impact usage numbers.

Make sure that you feel that on balance the benefit outweighs the impact.

## Implementation
We do not prescribe a particular implementation. Each team should determine which implementation is best suited for them. However, before selecting an implementation a team should be mindful of our working practices such as:

- [Graded Browser Support](https://github.com/springernature/frontend-playbook/blob/main/practices/graded-browser-support.md)
  - Is the implementation supported by all "enhanced" browsers? If not, is there a good justification for selecting it anyway?
  - Does the implementation work in conjunction with the Cut The Mustard technique?
- [Progressive Enhancement](https://github.com/springernature/frontend-playbook/blob/main/practices/progressive-enhancement.md)
  - This is not meant to force you to choose a non-js implementation, but rather for you to ensure you consider what will happen for users in varying circumstances from the beginning.
- [Our Performance Goals](https://github.com/springernature/frontend-playbook/blob/main/performance/performance-checklist.md)
  - What impact will the implementation have on the page performance of your site? 
  
## Quick Tips
Here are some quick suggestions for techniques that may prove useful:

### Understand the different user experiences in font loading: FOIT, FOUT and FOIT

- FOIT means flash of invisible text. When web fonts are loading, we hide text so users don’t see anything. We only show the text when web fonts are loaded.
- FOUT means flash of unstyled text. When web fonts are loading, we show users a system font. When the web font gets loaded, we change the text back to the desired web font.
- FOFT means flash of faux text. Only load the roman character set initially and load the others later for less page render blocking. "Faux" refers to the fact the browser fakes italics and bold before those character sets have loaded.

We believe that FOIT should be avoided as it is the worst experience for the user.

### Understand the different implementations available

We highly recommend reading [Zach Leat's comprehensive guide](https://www.zachleat.com/web/comprehensive-webfonts/) to get a good understand of the different techniques available. There is also a good [follow-up article](https://css-tricks.com/the-best-font-loading-strategies-and-how-to-execute-them/) that summarises Zach's findings.

### Serve WOFF and WOFF2 font formats

WOFF2 has the superior compression. However, unfortunately it does not cover all of our Enhanced browsers at the time of writing. Therefore consider serving both formats. 

### [font-display CSS](https://developer.mozilla.org/en-US/docs/Web/CSS/@font-face/font-display)

[`font-display`](https://developer.mozilla.org/en-US/docs/Web/CSS/@font-face/font-display) is useful and has the benefit of being a technique that does not require javascript and is easy and straight forward to implement.

`font-display: swap` can be used to achieve FOUT which ensures a user can read text with a fallback font whilst a webfont loads.

### Loading fonts with javascript

Consider using [FontFaceObserver](https://github.com/bramstein/fontfaceobserver) instead of the [CSS Font Loader API](https://drafts.csswg.org/css-font-loading/), as the latter does not have support for all our Enhanced browsers.

### Preloading webfonts

If you have to load a font the conventional way using a `<link>` then consider using the [preload technique](https://web.dev/preload-critical-assets/) to ensure the font is requested as early on in the page load process as possible. 

`<link rel="preload" href="HardingText-Regular-Web.woff2" as="font" type="font/woff2" crossorigin>`


### Self host webfonts if possible

Some webfonts prevent you from self hosting because of their licensing so check that first. But if you can, consider self hosting a font. As this will potentially reduce the possible points of failure or poor page performance. And it will open up more options to you in terms of possible font loading implementations.
