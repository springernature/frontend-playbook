# High magnification

Users with low vision may magnify the screen to be able to read text. Your web pages need to be responsive so that they allow these users to read text comfortably without horizontal scrolling or being impeded by design elements. 

To comply with WCAG 2.1 AA, you need to allow for up to 400% magnification. See [Understanding Success Criterion 1.4.4: Resize text
](https://www.w3.org/WAI/WCAG21/Understanding/resize-text.html) and [Understanding Success Criterion 1.4.10: Reflow
](https://www.w3.org/WAI/WCAG21/Understanding/reflow.html) for further details. 

## The issues

- [Content obscured at high magnification](#content-obscured-at-high-magnification)
- [Information removed at high magnification](#information-removed-at-high-magnification)

### Content obscured at high magnification

#### What's the problem?

When the screen is magnified, content is obscured. Text or functionality may be pushed off-screen. Elements may overlap with or cover up other elements. 

#### Who's affected by the problem?

* Low-vision users

#### Why's it a problem?

Low-vision users may need to zoom or magnify content in their browsers to be able to use a website. If content or functionality is obscured when they do this, they may be unable to read or use the website. 

#### How do I fix it? 

Use a [responsive design](https://www.smashingmagazine.com/2011/01/guidelines-for-responsive-web-design/). 

Make sure that nothing in your layout becomes visually obscured down to a width of 320px. 

### Information removed at high magnification

#### What's the problem?

When the screen is magnified (or when using a mobile layout), important information is removed. Text labels for icons may be removed from the UI, or menu items could be lost. 

#### Who's affected by the problem?

* Low-vision users
* Mobile device users

#### Why's it a problem?

Low-vision users may need to zoom or magnify content in their browsers to be able to use a website. In a responsively-designed website, this may effectively put them into the "mobile" layout. 

Removing information for visual effect may make it difficult for these users to interpret content, or move around the site effectively.

#### How do I fix it? 

Avoid "hiding" content in mobile layouts - if it's important enough to display on desktop, it's important enough to display on mobile. 

Make sure that the "mobile" content has parity with the "desktop" content. 