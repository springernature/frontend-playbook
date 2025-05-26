# The section element

- [What is the use case for a section element?](#what-is-the-use-case-for-a--section--element)
- [What facts should be considered before using an accessible section element?](#what-facts-should-be-considered-before-using-an-accessible-section-element)
- [What are the requirements for making a section element accessible](#what-are-the-requirements-for-making-a-section-element-accessible)
- [Testing for a correct section label](#testing-for-a-correct-section-label)


## What is the use case for a section element?

[The HTML spec of the Web Hypertext Application Technology Working Group (WHATWG)](https://html.spec.whatwg.org/multipage/sections.html#the-section-element) says: 

> The section element represents a generic section of a document or application. A section, in this context, is a
> thematic grouping of content, typically with a heading.

As a general rule, before using a section element, you should always think of a more specific element first, such
as article, aside, header, footer, nav, or main. If none of these are appropriate, you can use a section element
to point users of assistive technology (AT) to a relevant section of the page.

## What facts should be considered before using an accessible section element?

AT users who can use landmarks prefer a few well-chosen landmarks to many. And remember that a heading in
itself is a thing that an AT user can jump to directly - if you make all your sections landmarks using headings,
then you're just duplicating the headings in the landmark auditory interface, which makes the landmarks less
useful.

Caroly McLeod points out in [a post on w3c aria practices](https://github.com/w3c/aria-practices/issues/575#issuecomment-380620317):

> Happened to notice a trend in the WebAIM Screen Reader User Survey results: the use of landmark navigation is
> decreasing.
> 
> [Survey 5](https://webaim.org/projects/screenreadersurvey5/#landmarks): 44% of users always or often navigate by
> landmarks<br> 
> [Survey 6](https://webaim.org/projects/screenreadersurvey6/#landmarks): 39% of users always or often navigate by
> landmarks<br> 
> [Survey 7](https://webaim.org/projects/screenreadersurvey7/#landmarks): 31% of users always or often navigate by
> landmarks<br> 
> [Survey 8](https://webaim.org/projects/screenreadersurvey7/#landmarks): 27% of users always or often navigate by
> landmarks<br> 
> 
> If I had to guess why, I would say that it is most likely because landmarks are inconsistently implemented, and often
> over used. I would further guess that the lack of clarity in the spec(s) is contributing to this problem.

Furthermore, a W3C WAI-IG mailing-list thread “Landmarks without labels or no landmarks at all?” (Sept 2024) states:

> “Too many landmarks are super annoying and problematic… I generally advise avoiding nested landmarks and keeping the
> total in the range of 5 to 7.” – _Matt (blind screen-reader user)_<br>
>
> “Landmarks are supposed to be used sparingly … My main objection is the ‘noise’ that screen-reader users encounter.”
> – _Steve Green (screen-reader user & auditor)_<br>
> 
> [W3C Lists](https://lists.w3.org/Archives/Public/w3c-wai-ig/2024JulSep/0118.html)

Both explain that landmark “noise” slows them down - they only want a handful that map to genuinely major regions.

While many users of assistive technology use headlines to skim over a page, it may still make sense to use a headline to
label a section element, namely if it is important enough to be given its own landmark among the landmarks of the page.


## What are the requirements for making a section element accessible?

As Stefan Judis [explains in his article on section element accessibility](https://www.stefanjudis.com/today-i-learned/section-accessible-name/),
a "section" without an accessible name is nothing but a "div".

To make a section element accessible, you need to give it a label by adding a `aria-label` or `aria-labelledby`
attribute. This label should describe the content of the section in a way that is meaningful to assistive technology
users.

Without a label, the section element is assigned the role `generic` and is not announced by screen readers, making
it effectively invisible to assistive technology users. With a label, the section element is given the role `region`
and is announced by screen readers with the name of the label.

Example:

```html
<section aria-labelledby="headline-article-details">
  <h2 id="headline-article-details">Article details</h2>

  <dl>
        <dt class="c-submission-details__term">
            Corresponding author
        </dt>
        <dd class="c-submission-details__description">
            Charles Darwin
        </dd>
    </dl>
</section>
```


## Testing for a correct section label

You can test in Jest whether a section element has a proper label by checking that the `aria-labelledby` attribute is
set and that the referenced label element exists:

```javascript
describe('Your research section', () => {
    let sectionElement;
    let sectionLabelId;
    let sectionLabelElement;

    beforeAll(() => {
        sectionElement = document.querySelector('[data-test="your-research-section"]');
        sectionLabelId = sectionElement.getAttribute('aria-labelledby');
        sectionLabelElement = sectionElement.querySelector(`[id="${sectionLabelId}"]`);
    });

    it('exists', async () => {
        expect(sectionElement).not.toBe(null);
        expect(sectionLabelElement).not.toBe(null);
    });
});
```
