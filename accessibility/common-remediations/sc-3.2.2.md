# Success Criterion 3.2.2 On Input

The user must retain control over context changes so that they can be confident that the service will behave predictably. 

See [Understanding On Input](https://www.w3.org/WAI/WCAG22/Understanding/on-input.html) for further details. 

The issues and remediations listed in this file are not exhaustive. 

## The issues
- [No advance warning when opening new window](#no-advance-warning-when-opening-new-window)

### No advance warning when opening new window

#### What's the problem?

Links open in new window without warning the user that this will happen.

#### Who's affected by the problem?

* Screen reader users
* Low vision users who magnify the entire screen
* Users with cognitive challenges

#### Why's it a problem?

Having a window open unexpectedly when you click on a link can be disorientating to users who can only see a portion of the screen, who can't see the screen at all, or who can become easily distracted by unexpected changes to their browsing context. 

#### How do I fix it? 

Avoid opening links in new tabs or windows wherever possible. 

If you really have to do it, warn the user before they click on the link that it'll open in a new window. You can use text like "opens in a new window" or a visual icon. If you choose to use an icon, make sure it's accessible to screen reader users. 

You MUST use `rel="noopener"` on outbound links that open in a new window. See the [secure markup guide](https://github.com/springernature/frontend-playbook/blob/main/security/secure-markup.md#add-relnoopener-to-outbound-links-in-new-windows) for an explanation. 

We do this:
```html
<a href="https://mysite.com" target="_blank" rel="noopener">
   My site (opens in a new window)
</a>

 Or
 
<a href="https://mysite.com" target="_blank" rel="noopener">
   My site <img src="..." alt="opens in a new window"> 
</a> 
```

We don’t do this:
```html
<a href="knitting.html" target="_blank">All about Knitting</a>
```
