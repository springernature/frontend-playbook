# Keyboard navigation

All functionality must be available when using a keyboard alone. 

This allows users to operate the website using their keyboard or an alterate keyboard device or emulator. These may include speech input software, sip-and-puff software, on-screen keyboards, scanning software and a variety of assistive technologies and alternate keyboards. 

Keyboard navigation also benefits:

* People who are blind (who cannot use devices such as mice that require eye-hand coordination)
* People with low vision (who may have trouble finding or tracking a pointer indicator on screen)
* Some people with hand tremors or other motor issues who find using a mouse very difficult 

See [Understanding Guideline 2.1: Keyboard Accessible](https://www.w3.org/WAI/WCAG21/Understanding/keyboard-accessible) and its associated Success Criteria for further details. 

## The issues

- [Missing or inadequate focus styles](#missing-or-inadequate-focus-styles)
- [Visual order doesn't match source order](#visual-order-doesnt-match-source-order)

### Missing or inadequate focus styles

#### What's the problem?

Focus styles are missing from interactive elements, or are present but difficult to see. 

#### Who's affected by the problem?

* Keyboard users
* Low vision users browsing with a magnifier

#### Why's it a problem?

Not everyone uses a mouse. Some users navigate through a page with their keyboard by pressing the <kbd>tab</kbd> key to move from one focusable element to another. If focus styles are removed or insufficient, these users have no way of knowing which element they are about to activate. 

All elements that receive focus MUST have visible focus styles. 

Browser default focus styles are likely insufficient as they can be difficult to see in some designs. We prefer focus styles to be highly visible. 

#### How do I fix it? 

We do this:
```css
a:focus {
   outline: 3px solid #fece3e;
}

a:focus, button:focus {
   background-color: #fc0;
   outline: 2px solid #fc0;
}
```

We _don't_ do this:
```css
a:focus {
   outline: 0;
}
```

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
