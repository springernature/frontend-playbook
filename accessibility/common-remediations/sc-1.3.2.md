# Success Criterion 1.3.2 Meaningful Sequence

Content can be shifted around on screen using CSS or JavaScript so that it no longer matches the DOM order. This can be detectable to screen reader or other keyboard users who rely on the DOM to understand the sequence of the page. 

See [Understanding Meaningful Sequence](https://www.w3.org/WAI/WCAG22/Understanding/meaningful-sequence.html) and its associated Success Criteria for further details. 

The issues and remediations listed in this file are not exhaustive. 

## The issues

- [Visual order doesn't match source order](#visual-order-doesnt-match-source-order)

### Visual order doesn't match source order

#### What's the problem?

CSS positioning has been used so that the visual order of interactive elements doesn't match the HTML source order. 

#### Who's affected by the problem?

* Keyboard users
* Screen reader users

#### Why's it a problem?

Keyboard users (including screen reader users) expect to tab forwards and backwards through interactive elements in a linear sequence. For left-to-right languages, this means the elements should be presented in left-to-right order. 

Switching the visual order of elements with CSS but not changing the order in the source code can lead to focus being placed on unexpected elements, which can confuse users or cause them to activate the wrong control. 

For example, using a `float:right;` on an interactive element can make it visually appear to be the last control in a group, but when a keyboard user tabs into the component, it may be the first control they interact with. 

#### How do I fix it? 

* Take care when using CSS positioning, flexbox, and grid layouts
* Make sure the visual order of components matches the order in the HTML source
* Tab through your document to make sure the focus order is expected
* If the order of the content matters (e.g. an in-page navigation panel is only useful to a keyboard user if it appears before the main page content), amend the DOM structure accordingly

We do this:
```html
<button> I Should </button>
<button> Be focused</button>
<button> Last </button>
```

We don't do this:
```html
<button style=”float: right”> I Should </button>
<button> Be focused</button>
<button> Last </button>
```
