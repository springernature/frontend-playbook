A simple accessibility checklist
========================================

This checklist is a synthesis of the [Web Content Accessibility Guidelines 1], the [WCAG Samurai Errata], and one guideline from [Web Content Accessibility Guidelines 2].

It has proven helpful when building sites that comply with [US Section 508] and the [UK Equality Act 2010] \(all of our sites must comply with these pieces of legislation).

Be sure to create an issue or submit a pull request if you have any questions, or have spotted any improvements that can be made. 


1. **Where meaning would be lost if a non-text item were removed, has a text alternative been provided?**  
   [Samurai errata (guideline 1)](http://www.wcagsamurai.org/erratas/errata-listing/#GL1)

1. **Are audio and video accessible?**  
   [Samurai Errata (guideline 1, sound)](http://www.wcagsamurai.org/erratas/errata-listing/#sound)  
   [Samurai Errata (guideline 1, video)](http://www.wcagsamurai.org/erratas/errata-listing/#video)

1. **For actual content (in most cases, that means text), have confusable colours been avoided?**  
   For example, do not set light green text on a pink background.  
   There is no limitation on using confusable colours as design elements, nor is there a limitation on displaying areas of confusable colours next to each other (e.g., green type on a white background can sit alongside a solid red rectangle).  
   See this page about [effective colour contrast](http://powerplant.nature.com/wiki/display/JPCIS/Effective+colour+contrast).

1. **Has colour been avoided as a sole method of indicating an item on a page, either in its markup or style or via reference?**  
   For example, do not return a form with errors indicated solely in red; use additional markup, like strong, and/or use additional text like an asterisk or a visual icon with text equivalent, and/or explain in words what the errors are and where they are located.
   [Samurai Errata (guideline 2)](http://www.wcagsamurai.org/erratas/errata-listing/#GL2)

1. **Does text have a contrast ratio which makes it perceivable by people with colour blindness?**  
   The visual presentation of text and images of text has a contrast ratio of at least 4.5:1, except for the following:

   * Large Text: Large-scale text and images of large-scale text have a contrast ratio of at least 3:1;
   * Incidental: Text or images of text that are part of an inactive user interface component, that are pure decoration, that are not visible to anyone, or that are part of a picture that contains significant other visual content, have no contrast requirement.
   * Logotypes: Text that is part of a logo or brand name has no minimum contrast requirement.

   [WCAG 2 (guideline 1.4.3)](http://www.w3.org/TR/2008/REC-WCAG20-20081211/#visual-audio-contrast-contrast)

1. **Is the natural language of a page's text and any text equivalents (e.g., captions), identified through use of the lang attribute?**  
   For example: Identify the primary language of a document &ndash; preferably on the html tag, through use of the html lang attribute (or xml:lang attribute for xhtml). Where other languages are embedded within a document, an html lang attribute must be used (on an enclosing element) to indicate this.
   [Samurai errata (guideline 4)](http://www.wcagsamurai.org/erratas/errata-listing/#GL4)

1. **Have documents been organized so they may be read without style sheets?**  
   For example, when an HTML document is rendered without associated style sheets, it must still be possible to read the document. 
   [WCAG 1, guideline 6.1](http://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-order-style-sheets)

1. **Does the page transform gracefully?**  
   For example: Do not provide alternative presentations or alternate pages. Make the original page accessible. In particular, this requires you to use JavaScript or other scripting in a way that is intrinsically accessible. You are not required to create a single page that works exactly the same with and without scripting, nor should you create one page with scripting and another without it.  
   [Samurai Errata (guideline 6)](http://www.wcagsamurai.org/erratas/errata-listing/#GL6)

1. **Does the user have control of time-sensitive content changes?**  
   For example, do not cause flickering, flashing, or blinking. Advertisements, including advertisements served by a third party on a page you control, are covered by this guideline. They too may not cause flickering, flashing, or blinking.  
   [Samurai Errata (guideline 7)](http://www.wcagsamurai.org/erratas/errata-listing/#GL7)

1. **Are embedded elements of the interface accessible?**  
   For example: are programmatic elements such as scripts directly accessible? Are they device independent? Are they keyboard operable?  
   [WCAG 1, guideline 8](http://www.w3.org/TR/WCAG10/wai-pageauth.html#gl-own-interface)

1. **Has the page been designed for device-independence? E.g. is it keyboard accessible?**  
   For example: do not use server side image maps, do not use tabindex, do not use accesskey.  
   [Samurai Errata (guideline 9)](http://www.wcagsamurai.org/erratas/errata-listing/#GL9)  
   Also see [WCAG 1 glossary: "device independent"](http://www.w3.org/TR/WCAG10/wai-pageauth.html#device-independent)

1. **Are tables used appropriately?**  
   I.e. do data tables transform gracefully, and are layout tables absent?  
   [Samurai Errata (guideline 9)](http://www.wcagsamurai.org/erratas/errata-listing/#GL5)

1. **Have interim solutions been used?**  
   For example: have pop-ups been avoided? If opening new windows, is the user informed this will happen? If form placeholder text is used, is it done in an accessible way (e.g. using HTML5 placeholder attribute).  
   [Samurai Errata (guideline 10)](http://www.wcagsamurai.org/erratas/errata-listing/#GL10)

1. **Does the page Use W3C technologies and guidelines?**  
   For example: HTML for content, CSS for presentation.  
   [Samurai Errata (guideline 11)](http://www.wcagsamurai.org/erratas/errata-listing/#GL11)

1. **Has context and orientation information been provided?**  
   For example: have labels been explicitly associated with their controls?  
   Have large blocks of information been divided into groups, for example using fieldset, optgroup, nested lists, and headings?  
   [Samurai Errata (guideline 12)](http://www.wcagsamurai.org/erratas/errata-listing/#GL12)  
   Also see [WCAG guideline 12.3](http://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-group-information) and [WCAG guideline 12.4](http://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-associate-labels)

1. **Are there clear navigation mechanisms?**  
   For example: have "click here" type links been avoided? Are navigation mechanisms consistent? Has metadata been provided (e.g. microformats)? Is there a sitemap?  
   [WCAG guideline 13](http://www.w3.org/TR/WCAG10/wai-pageauth.html#gl-facilitate-navigation)

1. **Are documents clear and simple?**  
   For example: Has the clearest and simplest language been used for the page's content? Have graphic or auditory presentations been used (where they will facilitate comprehension)? Is there a style of presentation that is consistent across pages?  
   [WCAG 1, guideline 14](http://www.w3.org/TR/WCAG10/wai-pageauth.html#gl-facilitate-comprehension)  
   (Also see [WCAG 1 core technique 5: "Comprehension"](http://www.w3.org/TR/WCAG10-CORE-TECHS/#comprehension))

[US Section 508]: https://www.section508.gov/
[UK Equality Act 2010]: http://www.legislation.gov.uk/ukpga/2010/15/contents
[Web Content Accessibility Guidelines 1]: https://www.w3.org/TR/WCAG10/
[Web Content Accessibility Guidelines 2]: https://www.w3.org/TR/WCAG20/
[WCAG Samurai Errata]: http://www.wcagsamurai.org/erratas/introduction/
