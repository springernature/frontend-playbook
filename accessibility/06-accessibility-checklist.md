# A simple accessibility checklist

This checklist aims to help you and your team create accessible products. It's heavily inspired by Vox Media's [Accessibility Guidelines](http://accessibility.voxmedia.com/).

- [Semantics and structure](#semantics-and-structure)
- [Media](#media)
- [Colours](#colours)
- [Interactivity](#interactivity)
- [Forms](#forms)
- [Content](#content)


## Semantics and structure

### Use the correct HTML element

Browsers build the [accessibility tree](https://developer.paciellogroup.com/blog/2015/01/the-browser-accessibility-tree/) by making assumptions about page elements and the sort of content they are likely to contain.

Using the correct HTML elements helps the browser make sense of your page, and helps assistive technology users navigate it more easily.

Resources:

* [Article: Semantic structure](https://webaim.org/techniques/semanticstructure/)


### Use HTML landmarks

Assistive technology may make use of ARIA landmark roles or HTML5 landmark elements for navigation. These allow users to quickly jump between page sections.

There are [8 landmark roles](https://developer.mozilla.org/en-US/docs/Web/Accessibility/ARIA/Roles#3._landmark_roles). Most browsers implicitly detect these roles if you use the correct HTML5 semantic element, but you may need to add the appropriate ARIA `role=` if you have to support an older browser.

If you use more than one landmark of the same type, give each landmark a unique label so that screen reader users can tell them apart easily.

Resources:

* [Article: WAI finding with ARIA landmark roles](http://alistapart.com/column/wai-finding-with-aria-landmark-roles)
* [Article: Labeling Regions](https://www.w3.org/WAI/tutorials/page-structure/labels/)
* [Video: How ARIA landmark roles help screen reader users](https://www.youtube.com/watch?v=IhWMou12_Vk&feature=youtu.be)
* [Tool: Landmarks extension for Chrome, Firefox and Opera](http://matatk.agrip.org.uk/landmarks/)
* [Tool: HTML5 accessibility feature support for sections](http://www.html5accessibility.com/#sections)


### Provide skip links to bypass repetitive content

Not all users are able to easily navigate by landmarks. Multiple navigation links typically found at the top of a document all have to be laboriously tabbed through using a keyboard, on every page the user visits.

To help them out you can add a "Skip Navigation" link to the top of each page which, when activated, will take them to the main section of the page.

The Elements Design System includes [a skip link implementation](https://elements.springernature.com/springernature/components/global-skip-link) that you can use in your own project(s). 

Resources:

* [Article: WebAIM's overview of Skip Navigation techniques](https://webaim.org/techniques/skipnav/)


### Declare a language attribute

Declaring a language attribute on the HTML element allows a screen reader to read out text with correct pronunciation. It also helps search engines return language-specific results.

If you include text on a page that uses a different language to the main document (e.g. your HTML lang is `en` and you are including a passage in `jp`), also identify that text with its own lang attribute.

We do this:

```
<p>This document has the lang="en" attribute, and this text matches the document language.</p>
<p lang="jp">このテキストは日本語です</p>
```

Resources:

* [Article: Using the HTML lang attribute](https://developer.paciellogroup.com/blog/2016/06/using-the-html-lang-attribute/)


### Use a logical source order

Your page should still make sense when you look at it without CSS. This is a core [progressive enhancement technique](../practices/progressive-enhancement.md).

Don't surprise users by using CSS to make changes to apparent source order, e.g. by using floats and absolutely-positioned elements.

Flexbox and CSS grids are particularly vulnerable to apparent source order surprises, and you should take extra care when using them.

Resources:

* [Article: Logical document structures](http://www.bettertesting.co.uk/content/?p=1619)
* [Article: Source order matters](http://adrianroselli.com/2015/09/source-order-matters.html)
* [Tool: Wave Extension](https://wave.webaim.org/extension/)


### Use headings correctly

The [HTML5 outline algorithm](https://developer.mozilla.org/en-US/docs/Web/Guide/HTML/Using_HTML_sections_and_outlines) can't yet be relied on to convey information to users. Freely use HTML5 sectioning elements, but use headings to define the structure of your document. In basic terms this means one H1 per page! See our [HTML markup house style](https://github.com/springernature/frontend-playbook/blob/main/markup/house-style.md#follow-the-html-4-outline-model-for-heading-levels) for more information on the outline algorithm and why we don't use multiple level one headings.

Use an appropriate heading for each section. You can visually hide headings, but make sure they're still accessible to screen reader users.

Don't skip heading levels.

Resources:

* [Article: Heading structures are tables of contents](https://hiddedevries.nl/en/blog/2018-09-01-heading-structures-are-tables-of-contents)
* [Article: Semantic Structure](https://webaim.org/techniques/semanticstructure/)


### Use progressive enhancement

Progressive enhancement means starting with a logical and semantic HTML document with all key functionality, then enhancing it with an aesthetic layer (CSS) and behavioural layer (JavaScript). It has benefits beyond accessibility but is a key starting point for creating accessible experiences.

Resources:

* [Playbook: Progressive enhancement](../practices/progressive-enhancement.md)


## Media

### Audio or video elements must be accessible

This could involve adding [captions to videos](https://www.youtube.com/watch?v=5AXApBbj1ps), providing [transcripts of audio content](https://www.nature.com/articles/d41586-021-01491-0), including audio description on videos, or including a text alternative for videos that have no audio track.

Automatic captions (e.g. those provided by YouTube) are insufficient for accessibility compliance.


### Provide text alternatives for images

Alt attributes should describe the image they're applied to. E.g. the alt attribute for a photograph should describe what's happening in the photograph, not just say "photograph".

Screen reader users prefer alt text to be short and informative. Avoid redundant phrases like "image of...", and try to keep the total text under 125 characters. Don't use the `longdesc` element for longer descriptions - its browser support is patchy and there are better-supported alternatives.

If an image provides no information, is purely decorative, and can't be moved from HTML into CSS, an empty alt attribute (`alt=""`) is preferred.

Resources:

* [Article: How to Design Great Alt Text](https://www.deque.com/blog/great-alt-text-introduction/)
* [Article: Alternative Text](https://webaim.org/techniques/alttext/)
* [Article: How long can an "alt" attribute be?](https://www.washington.edu/accessit/print.html?ID=1257)
* [Article: Longdesc alternatives in HTML5](https://cookiecrook.com/longdesc/)


## Colours

### Use adequate colour contrast

Text and images of text must have a colour contrast ratio of at least 4.5:1.

Don't use confusable colours. Make sure your choices can be perceived by people with colour blindness.

Resources:

* [Article: Colour contrast - why does it matter?](https://accessibility.blog.gov.uk/2016/06/17/colour-contrast-why-does-it-matter/)
* [Tool: Color Contrast Checker](https://webaim.org/resources/contrastchecker/)
* [Tool: Funkify](http://www.funkify.org/)
* [Tool: Visbug extension for Chrome](https://chrome.google.com/webstore/detail/visbug/cdockenadnadldjbbgcallicgledbeoc)


### Don't convey information with colour alone

Use text equivalents or semantic emphasis like `<strong>` or `<em>` when conveying important information to users. No hyperlinks may be indicated by text color alone. Except in special cases, such as options in navigation menus, use an underline.

Resources:

* [Article: Don’t use color alone to convey meaning](http://universalusability.com/access_by_design/color/alone.html)
* [Why you should (almost) always underline your links](https://www.tempertemper.net/blog/why-you-should-almost-always-underline-your-links)


## Interactivity

### Give enough time to read and use content

Let the user pause, stop, or hide content that moves, blinks, scrolls, or automatically updates.

Resources:

* [Case studies: How People with Disabilities Use the Web](https://www.w3.org/WAI/intro/people-use-web/principles#time)

### Disable webfonts and animations when `prefers-reduced-motion` is selected

Operating systems allow users to indicate that they prefer reduced motion. This is helpful for users with vestibular disorder, anxiety, dizzyness, etc. This choice is exposed in browsers by using the [`prefers-reduced-motion`](https://developer.mozilla.org/en-US/docs/Web/CSS/@media/prefers-reduced-motion) media query.

Make sure that all animations, including loading of webfonts (which can cause FOUT), are disabled when `prefers-reduced-motion` is selected.

Resources:

* [Article: Introduction to Reduced Motion Media Query](https://css-tricks.com/introduction-reduced-motion-media-query/)
* [Article: Revisiting prefers-reduced-motion](https://css-tricks.com/revisiting-prefers-reduced-motion-the-reduced-motion-media-query/)
* [Article: Prefers reduced motion](https://developers.google.com/web/updates/2019/03/prefers-reduced-motion)

### Design for device independence

Make sure users can interact with your page using the keyboard alone.

Don't rely on device-dependent event handlers (e.g. `onhover`) as the sole method to convey information or to complete tasks.

Make sure interactable elements are large enough for touchscreen users to easily access controls. Leave enough space around controls so that they don't overlap with other touch targets.

Resources:

* [Article: Touch Target Sizes](https://www.lukew.com/ff/entry.asp?1085)


### Give context and orientation information

Give users a way to know where they are in a set of related pages (e.g. the [Steps Left pattern](http://ui-patterns.com/patterns/StepsLeft)).

Make sure the currently-focused element has a focus ring, and make sure the focus sequence is logical.

### Avoid opening links in new windows

This can be disorientating to screen reader users or users with cognitive disabilites.

If you must do it, warn the user _before_ they click on the link that it'll open in a new window. You can use visible text like "opens in a new window" or a visual icon. If you choose to use an icon, make sure it's accessible to screen reader users.

Resources:

* [Article: Link Targets and 3.2.5](https://adrianroselli.com/2020/02/link-targets-and-3-2-5.html)
* [Article: How to Stop Opening Links in New Windows without Warning](https://knowbility.org/blog/2019/links-opening-new-windows-no-warning)
* [Article: Should links open in new windows?](https://www.smashingmagazine.com/2008/07/should-links-open-in-new-windows/)


## Forms

### Labels and context

* Associate all form controls with appropriate labels.
* Use fieldsets or optgroups to group related controls.

### Don't use HTML5 input placeholders for important information

Input placeholders disappear when the user begins typing, may be mistaken for a value, and may not provide adequate context.

Never put user instructions in input placeholders - always use a label. The HTML5 specification clarifies that a placeholder should not be used as an alternative to a label.

Resources:

* [HTML5 Living Specification: the placeholder attribute](https://html.spec.whatwg.org/dev/input.html#the-placeholder-attribute)
* [Article: HTML5 Accessibility Chops: the placeholder attribute](https://developer.paciellogroup.com/blog/2011/02/html5-accessibility-chops-the-placeholder-attribute/)
* [Article: 11 reasons why placeholders are problematic](https://medium.com/simple-human/10-reasons-why-placeholders-are-problematic-f8079412b960)
* [Article: Don’t Use The Placeholder Attribute](https://www.smashingmagazine.com/2018/06/placeholder-attribute)

### Help users make the most of autocomplete and autofill

By default, browsers remember information that users submit into input fields. The browser can then suggest possible completions for fields that the user has started typing in (autocomplete) or pre-populate certain fields when the page loads (autofill). This behaviour can be turned off in HTML with the `autocomplete="false"` attribute.

Don't indiscriminately disable autocomplete for input fields. The default autocomplete and autofill behaviours are useful for many users with and without disabilities.

For example, autocomplete helps users with motor disabilities by reducing the amount of typing they need to do in input fields. Autofill can help users with cognitive disabilities by automatically filling in common information like addresses or telephone numbers.

Don't disable autocomplete on sensitive fields like username and password fields. Any security benefits of doing this is negligible compared to the benefits of users' in-browser password managers, and has a direct negative impact on accessibility. Read the note on autofill in the [secure markup guide](https://github.com/springernature/frontend-playbook/blob/main/security/secure-markup.md#a-note-on-autofill) for more on that.

For fields where the user is expected to input information _about themselves_, use a valid autocomplete value if one exists - this helps make form filling software more effective. The HTML specification provides a [list of valid autocomplete values](https://www.w3.org/TR/html53/sec-forms.html#sec-autofill).

Don't use autocomplete values on input fields where the user is expected to input one-time information about _somebody else_ (e.g. a teacher filling out a form with the details of a list their students).

Resources:

* [Article: Making password managers play ball with your login form](https://hiddedevries.nl/en/blog/2018-01-13-making-password-managers-play-ball-with-your-login-form)
* [Understanding WCAG 2.1: Success Criterion 1.3.5: Identify Input Purpose](https://www.w3.org/WAI/WCAG21/Understanding/identify-input-purpose.html)
* [MDN reference: The HTML autocomplete attribute](https://developer.mozilla.org/en-US/docs/Web/HTML/Attributes/autocomplete)

## Content

### Use link text that makes sense out of context

Screen reader users may navigate a page by links alone. Avoid link text that says "click here", or context-free text like "More details" repeatedly applied to a list of links.

Resources:

* [Article: Writing good link text](https://www.nomensa.com/blog/how-write-good-link-text)


### Use tables appropriately

Don't use tables for layout. If a data table lacks important characteristics like `<th>` elements, some assistive technology may treat it as though it's a layout table and read its contents linearly. This can make it much more difficult for a screen reader user to understand.

Resources:

* [Article: Creating Accessible Tables](https://webaim.org/techniques/tables/)

