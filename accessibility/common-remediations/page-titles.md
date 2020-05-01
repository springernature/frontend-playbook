# Page titles

The HTML `<title>` element provides vital information to many users about the purpose and identity of your pages. Page titles must be provided, unique, and useful. 

## The issues

- [Title doesn’t describe the page](#title-doesnt-describe-the-page)
- [Same title used on multiple pages](#same-title-used-on-multiple-pages)

### Title doesn’t describe the page

#### What's the problem?

The `<title>` element fails to describe the purpose of the page. You may have failed to add a title, used title text that is too generic to be useful, or used an excessively long title that obscures the page purpose. 

#### Who's affected by the problem?

* Everyone

#### Why's it a problem?

When your page titles are inadequate:

* Screen reader users are unable to know what the point of a page is without scanning its entire contents
* All users are unable to easily find the correct tab if they temporarily change contexts
* All users who bookmark the page with their browser are given a poor default name for the bookmark
* Search engines may only display the first 50-60 characters of the title attribute, so information could be lost in [SERPs](https://en.wikipedia.org/wiki/Search_engine_results_page)

#### How do I fix it? 

All page titles must clearly summarise the purpose of the page. Front-load the most important information about the page so that it appears first. 

We do this:
```html
<title>Career opportunities | Website.com </title>
<title>Contact us | Website.com </title>
```
 
We _don’t_ do this:
```html
<title>Website.com</title>
<title>Website</title>
<title>Website.com sells vital products in very important markets to our many happy customers | Contact Us</title>
```

### Same title used on multiple pages

#### What's the problem?

The `<title>` attribute fails to differentiate the purpose of the page. 

#### Who's affected by the problem?

* Everyone

#### Why's it a problem?

When your page titles are the same on every page:

* Screen reader users are unable to know what the point of a page is without scanning its entire contents
* All users are unable to easily find the correct tab if they temporarily change contexts
* All users who bookmark the page with their browser are given a poor default name for the bookmark

#### How do I fix it? 

Where pages are unique, their titles must also be unique. The page title should usually match the main heading (h1) of the page.

We do this:
```html
<title>Checkout | Billing information | My webpage </title>
<title>Checkout | Review Cart | My webpage </title>
```

We _don’t_ do this:
```html
<title>Checkout | My webpage</title>
```
