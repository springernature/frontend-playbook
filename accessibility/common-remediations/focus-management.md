# Focus management

"Focus management" is the practice of setting the user's current focus programmatically. You might need to do this when you change the user's context in response to an action they triggered, such as changing a page view or interacting with a complex component. 

## The issues

- [No focus management](#no-focus-management)
- [Inappropriate use of `autofocus`](#inappropriate-use-of-autofocus)
- [Focus fails to return to triggering element](#focus-fails-to-return-to-triggering-element)

### No focus management

#### What's the problem?

Programmatic focus is absent. You may have written an SPA that fails to handle focus management automatically, or you may have neglected to implement programmatic focus on a component that changes the user's context (e.g. a modal dialog, a menu, or a custom page scrolling system).

#### Who's affected by the problem?

* Screen readers
* Keyboard users

#### Why's it a problem?

"Focus management" is the practice of setting the user's current focus programmatically. 

Most SPA frameworks fail to handle this automatically, and you need to implement it yourself. When a user activates a control to trigger a route change, the view visually updates. When you don't implement focus management, screen reader users are not made aware that the context has changed, and are left guessing whether or not activating the control did anything. Keyboard users may be able to see the visual changes, but they're left with their keyboard focus still on the trigger control. The control is no longer visible on the screen and may require additional, unnecessary work from the keyboard user to get reoriented. 

Implementing ARIA patterns that require focus management (e.g. modal dialogs or menus, among others), but neglecting to implement that focus management can also confuse users or prevent them from being able to use your document.  

Scroll hijacking ("scrolljacking") or custom scrolling components can allow a user to click on a navigation item, but fail to set their focus to the correct location. Screen reader users and and keyboard users are left to tab through the entire document to get to the section that they want to use, instead of having their focus placed there automatically. 

#### How do I fix it?

Watch this video by Google Developer Advocate Rob Dodson on [Managing Focus (7:23)](https://www.youtube.com/watch?v=srLRSQg6Jgg&list=PLNYkxOF6rcICWx0C9LVWWVqvHlYJyqw7g&index=23&t=0s) for a demonstration of the problem and an explanation of how to fix it in a broad range of contexts. 

If you're building a component that has an ARIA pattern (e.g. a modal dialog), follow the ARIA specification for the pattern you're using. Watch this video by Rob Dodson on [Accessible Modal Dialogs (12:45)](https://www.youtube.com/watch?v=JS68faEUduk&list=PLNYkxOF6rcICWx0C9LVWWVqvHlYJyqw7g&index=19) to see an example of how to apply the ARIA specification to a modal dialog. 

If you're building a SPA with a JavaScript framework, check for the correct way to enable focus management on router view changes. Read [Single Page Apps routers are broken](https://medium.com/@robdel12/single-page-apps-routers-are-broken-255daa310cf) by Robert DeLuca to get some suggestions that may work for your framework. 

### Inappropriate use of `autofocus`

#### What's the problem?

The `autofocus` attribute in a form field has been used to programmatically set focus in a way that's detrimental to the user experience. 

#### Who's affected by the problem?

* Screen reader users
* Keyboard users
* Touch device users
* Low vision users

#### Why's it a problem?

The `autofocus` attribute can be used to programmatically set the user's focus to a specific form field. 

If the field is not the only thing on the page, or if it comes after a number of other controls or pieces of content, screen reader users may miss all of the content that precedes the field. 

Keyboard users may be confused about the location of their focus, expecting it start at the top of the screen, and may become frustrated if they can't orient themselves. 

The autofocus behaviour can cause dynamic keyboards to display on some touch devices. In some cases, the autofocus behaviour can cause the browser to automatically scroll to the automatically-focused form field, disorienting users who can only see a portion of the screen (e.g. low vision users browsing at high magnification). 

#### How do I fix it?

The `autofocus` attribute is rarely helpful. If the user can perform multiple tasks on the page, or if the automatically-focused form field comes after other page content, then the `autofocus` attribute should not be used. 

### Focus fails to return to triggering element

#### What's the problem?

Upon some interaction, focus has been programmatically placed inside a component. When that component is closed, the user's focus is not returned to where it was before the new behaviour was triggered. 

#### Who's affected by the problem?

* Keyboard users
* Screen reader users

#### Why's it a problem?

Users expect consistency in an interface. Sometimes you need to programmatically set a user's focus in a component so they can carry out a task. If you don't return their focus afterwards to what they were doing before, it can be very confusing for users who navigate with the keyboard. 

If focus is placed on an unexpected or unrelated element, then the user might activate the wrong thing or struggle to work out where they are on the page. 

If focus is kept on a component that has been moved off-screen or hidden, a keyboard user will have a difficult time working out how they can get back to interacting with the visible components. 

If focus is lost entirely, then the browser will automatically return it to the top of the page. Keyboard and screen reader users will have a frustrating time getting back to where they were before you interrupted them. 

#### How do I fix it? 

Whenever you use programmatic focus to orient a user in some component (e.g. a menu or a modal dialog), make sure that their focus is returned to the invoking element when that component is closed. For example, if the component was invoked by activating a button, when the component is closed, focus must be returned to that button. 

If there was no invoking element (e.g. your component automatically appears when some JavaScript loads), return the user's focus to whatever they were interacting with before you manipulated their focus. 