# Semantics

Using the correct semantics in your HTML is vital if your page is going to work with technology that interfaces with it. At the most basic level, this means browsers themselves, but it's also required for assistive technology, search engines, third party content readers, virtual assistants like Siri or Cortana, and any other technical interface that can read and repurpose a webpage. 

## The issues

- [No built-in semantics](#no-built-in-semantics)
 
### No built-in semantics

#### What's the problem?

HTML elements with no semantics (`<div>`s and `<span>`s) have been used instead of elements with the correct semantics. The elements may be styled with CSS to look like semantic elements, and/or have JavaScript functionality attached that makes them perform in a similar way to a native element, but the correct native element has not been used. 

#### Who's affected by the problem?

* Everyone

#### Why's it a problem?

HTML elements with no semantics are not understood or handled automatically by user agents. Unless you fully understand the entire specification for a native element (such as a `<button>`), and implement it precisely to that specification, your attempts to replicate its functionality robustly for all users will fail. 

Screen reader users, voice input users, keyboard users, switch device users, users of other kinds of Assistive Technologies, search engines, various types of automated testing software, among others, are likely to be unable to use your interface if you use unsemantic elements. 

#### How do I fix it?

* Use native HTML elements unless you have a very good reason not to
* Make sure you are using the correct native HTML element for the purpose
 
We do this:

```html
<button>Toggle UI</button>
<a href=”/”>Visit this location</a>
<h2>This is a level 2 heading</h2>
```

We _don’t_ do this:

```html
<div onclick=”doFunc();”>Toggle UI</div>
<span>Visit this location</span>
<span>This is a level 2 heading</span>
```