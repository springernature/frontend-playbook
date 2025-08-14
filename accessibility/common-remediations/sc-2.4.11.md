# Success Criterion 2.4.11 Focus Not Obscured (Minimum)

Keyboard focus must be visible - if a sighted keyboard user can't see a focus ring or similar focus styling, they will be unable to locate themselves on the page.

See [Understanding Focus Not Obscured (Minimum)](https://www.w3.org/WAI/WCAG22/Understanding/focus-not-obscured-minimum.html) for further details. 

The issues and remediations listed in this file are not exhaustive. 

## The issues

- [Missing or inadequate focus styles](#missing-or-inadequate-focus-styles)

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

