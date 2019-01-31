# Browser support

This page describes the way that we support different browsers and browser versions when building sites at Springer Nature.

* [Our criteria for browser support](#our-criteria-for-browser-support)
* [Browser support list](#browser-support-list)
* [Implementing browser support](#implementing-browser-support)
  * [Implementation details](#implementation-details)
  * [Caveats](#caveats)
    * [Internet Explorer 10 support](#internet-explorer-10-support)
    * [Internet Explorer and CSS Grid](#internet-explorer-and-css-grid)
    * [Browsers without TLS 1.2 support](#browsers-without-tls-1.2-support)

## Our criteria for browser support

We follow the principles of [Progressive Enhancement](progressive-enhancement.md) and implement it at the broadest level using using a variant of [Yahoo's Graded Browser support](https://github.com/yui/yui3/wiki/Graded-Browser-Support) (a concept originally conceived by [Nate Koechley](https://web.archive.org/web/20060304042737/http://developer.yahoo.net/yui/articles/gbs/gbs.html).

Our approach to browser support works by classifying all versions of all browsers into one of two grades:

* **"Core"** is our universal support grade. We serve all browsers at this grade server-side rendered semantic HTML and minimal CSS. Essential user journey's must be accessible at this grade.
* **"Advanced"** is our support grade for modern and/or [evergreen browsers](https://www.techopedia.com/definition/31094/evergreen-browser). As well as the Core HTML and CSS, we serve these browsers JavaScript and more advanced CSS, giving them a more interactive and visually pleasing product experience. Bugs at this level are addressed with high priority.

## Rationale

We have two core reasons for this:

* We wish to support all users. No matter their device, browser, or network condition, the user should find a working and robust product.
* We wish to keep support costs low. Given the previous statement, we do not want to spend significant time [making advanced CSS and JavaScript work in older browsers](https://en.wikipedia.org/wiki/Pareto_principle#In_software).

## Browser support list

This is the current list of browser versions and their corresponding grades:

| Browser         | Advanced                        | Core               |
| --------------- |:-------------------------------:| ------------------:|
| Chrome          | latest stable, latest stable -1 | < 29               |
| Edge            | latest stable, latest stable -1 | n/a                |
| Firefox         | latest stable, latest stable -1 | < 29               |
| IE              | 11                              | < 11               |
| Opera           | latest stable                   | < 16               |
| Safari iOS      | latest stable, latest stable -1 | < 7                |
| Safari MacOS    | latest stable, latest stable -1 | < 6.1              |
| Android Webview | latest stable                   | < 30 (Android 4.4) |

### Grey area browsers

Some browser versions exist in the grey area outside and/or between Advanced and Core grades. For example:

* Old versions of an evergreen browser: a user has turned off auto-updates, or their upgrade opportunities are limited by their device or administrator.
* Nightly or developer versions of evergreen browsers.

We serve these grey area browsers the Advanced version of a site, so they will receive the full experience. Due to resourcing implications we do not specifically test our products against them - however we do expect them to work. Over time, analysis of errors and usage patterns may cause some browsers in this grey area to be deliberately changed to either Advanced or Core, to allow for better support.

## Implementing browser support

Our primary approach to classifying a browser support level is the "[Cutting the Mustard (CTM)](http://responsivenews.co.uk/post/18948466399/cutting-the-mustard)" progressive enhancement technique, based upon the principles developed by the BBC.

This approach works by using feature detection in order to determine which browsers will receive the full Advanced experience (i.e. they "[cut the mustard](https://en.wiktionary.org/wiki/cut_the_mustard)") and which ones will receive only the Core experience.

### Implementation details

All browser versions load a basic stylesheet that contains only [normalisation](https://necolas.github.io/normalize.css/) and a few small enhancements to the user-agent stylesheet (typically max-width layout and colour and logo branding).

We then use CSS media queries to detect capable browsers. Unlike the approach described by the BBC, we don't use a JavaScript-based featured detection. We want users to have the best possible experience even if JavaScript is not available.

To load the full experience only in Advanced browsers we implement logic in the media attribute of the `<link>` element that identifies the main stylesheet, loading the stylesheet only in browsers that recognise the properties of that media query:

```html
<link rel="stylesheet" href="advanced.css" media="only screen and (-webkit-min-device-pixel-ratio:0) and (min-color-index:0), (-ms-high-contrast: none), only all and (min--moz-device-pixel-ratio:0) and (min-resolution: 3e1dpcm)" id="advanced-stylesheet">
```

This technique is documented in [Cutting the Mustard with Media queries](https://www.sitepoint.com/cutting-the-mustard-with-css-media-queries/). The specific media queries we use are based upon [CSS Only Mustard Cut](https://github.com/Fall-Back/CSS-Mustard-Cut), with a preference towards combining them into one rather than separating them out into multiple `<link>` elements. Note that you **cannot** add line breaks to the media query if they are combined.

We couple the loading of JavaScript to the loading of the enhanced CSS. We use the [window.matchMedia](https://developer.mozilla.org/en/docs/Web/API/Window/matchMedia) API to detect when the browser loads the CSS within the media query. Once the enhanced CSS loads, this will cause the JavaScript code to load too.

```javascript
(function() {
  var linkEl = document.getElementById('advanced-stylesheet');
  if (window.matchMedia && window.matchMedia(linkEl.media).matches) {
    var script = document.createElement('script');
    script.src = 'advanced-script.js';
    script.async = true;
    document.body.appendChild(script);
  }
})();
```

### Caveats

#### Internet Explorer 10 support

As of January 2017, we consider Internet Explorer 10 a Core browser. This is mainly due to its lack of support for certain modern features plus very low usage numbers. IE10 also stopped receiving security updates in January 2016 from its manufacturer.

Unfortunately, both IE10 and IE11 respond to the same CSS media queries, which means that it is not possible to use a CSS-only method of differentiating between both browsers.

This means that even if we consider IE10 a Grade-C browser, we currently serve IE10 users the full experience.

#### Internet Explorer and CSS Grid

[CSS Grid](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Grid_Layout) has been available in all evergreen browsers [for the last year](https://caniuse.com/#feat=css-grid). It offers a much-simplified way of working with layout and offers new design opportunities.

However, CSS Grid is not available in the full standardised form in Internet Explorer 10 or 11, both of which are currently supported *de facto* as Advanced browsers (see above).

The syntax and capabilities for CSS Grid are radically different in IE than in any other browser. As a result the development costs to match the visual experience in IE with other browsers can range from trivial, for simple component-level layouts, to major for page-level layouts.

We therefore accept that some teams will wish to develop their layouts using CSS Grid, but will not be able to justify devoting time to supporting IE. For those teams we suggest a highly-styled linear layout, which has all the features of an Advanced browser experience, except for the page layout. It is up to any teams making this decision to ensure the IE10/11 Advanced experience is acceptable to their users and business owners.

#### Browsers without TLS 1.2 support

As of June 2018, all our sites are served through HTTPS using the [TLS 1.2 cryptographic protocol](https://en.wikipedia.org/wiki/Transport_Layer_Security#TLS_1.2) or newer. This means that users of browsers that don't support TLS 1.2 (e.g. Safari on iOS 4) will not be able to access our sites. Browsers that have support for TLS 1.2 not enabled by default (e.g. Internet Explorer on Windows 7) will not be able to access our sites, unless they change their default settings. We consider that this is required in order to keep our users secure.

The way that we restrict the connection to our sites when not using TLS 1.2 doesn't impact the way that we design and build our sites and our commitment to an approach based on progressive enhancement techniques.
