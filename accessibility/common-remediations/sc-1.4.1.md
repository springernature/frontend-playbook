# Success Criterion 1.4.1 Use of Color

Partial sight, aging and congenital color deficits all produce changes in perception that reduce the visual effectiveness of certain color combinations. 

See [Understanding Use of Color](https://www.w3.org/WAI/WCAG22/Understanding/use-of-color.html) for further details. 

The issues and remediations listed in this file are not exhaustive. 

## The issues

- [Information conveyed by colour alone](#information-conveyed-by-colour-alone)

### Information conveyed by colour alone

#### What's the problem?

Some kind of information is conveyed with colour, with no supplementation in text or by some other method. 

Examples may include (but are not limited to):

* Changing the background colour of an input field to red to indicate an error without also providing an error message
* Changing the colour of an icon or text string to indicate some kind of status
* Using a graph or a chart where colour is the only way to indicate different aspects of the data
* Removing underlines from hyperlinks, leaving just colour to differentiate them from surrounding text

#### Who's affected by the problem?

* Screen reader users
* Users with colour blindness
* Low-vision users who use high contrast modes
* Users with monochromatic displays or displays with inaccurate colour reproduction
* All users if a stylesheet containing colour information fails to load for any reason (network problems, server issues, etc.)

#### Why's it a problem?

Screen reader users without a display can never see colour, and nor can users who are experiencing problems loading your stylesheets. 

Colour blind or high contrast display users may not perceive colours in the way you intended, and in some cases may be unable to perceive your colour choices at all. 

Any kind of information that's only conveyed using colour can't convey that information if the colour isn't perceivable by the user. 

#### How do I fix it? 

You can use colour to indicate statuses or differences, but supplement it with something else. 

This can include (but is not limited to):

* Text labels and descriptions
* Error messages presented in text

In charts or graphs:

* Consider using a monochrome colour palette
* Use different [relative luminance](https://developer.mozilla.org/en-US/docs/Web/Accessibility/Understanding_Colors_and_Luminance) for different data points
* Use different fill patterns in addition to solid colour areas
* Use unambiguous text labels for lines or bars

For links:

* Never indicate a link with `color` alone
* Use `text-decoration: underline` (automatically applied by user agents) in all but special cases, such as navigation menus
