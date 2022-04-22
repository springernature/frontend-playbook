# Browser support

This page describes the way that we support different browsers and browser versions when building sites at Springer Nature.

* [Our criteria for browser support](#our-criteria-for-browser-support)
* [Browser support list](#browser-support-list)
* [Implementing browser support](#implementing-browser-support)
  * [Implementation details](#implementation-details)
  * [Caveats](#caveats)
    * [Browsers without TLS 1.2 support](#browsers-without-tls-1.2-support)

## Our criteria for browser support

We follow the principles of [Progressive Enhancement](progressive-enhancement.md) and implement it at the broadest level, using a variant of [Yahoo's Graded Browser support](https://github.com/yui/yui3/wiki/Graded-Browser-Support) (a concept originally conceived by [Nate Koechley](https://web.archive.org/web/20060304042737/http://developer.yahoo.net/yui/articles/gbs/gbs.html)).

Our approach to browser support works by classifying all versions of all browsers into one of two levels:

* **"Core"** is our universal support level. We serve all browsers at this level server-side rendered semantic HTML and minimal CSS. Essential user journey's must be accessible at this level.
* **"Enhanced"** is our support level for modern and/or [evergreen browsers](https://www.techopedia.com/definition/31094/evergreen-browser). As well as the Core HTML and CSS, we serve these browsers JavaScript and more advanced CSS, giving them a more interactive and visually pleasing product experience. Bugs at this level are addressed with high priority.

## Rationale

There are two motivators for approaching browser support like we do:

* We must support all users. No matter their device, browser, or network condition, the user should find a working and robust product.
* We should apply effort efficiently. It is both impractical _and_ counterproductive [making advanced CSS and JavaScript work in older browsers](https://en.wikipedia.org/wiki/Pareto_principle#In_software). Attempting to do so results in fragile sites, code bloat, and no benefit for users.

## Browser support list

This is the current list of browser versions and their corresponding support level:

| Browser           | Enhanced           | Core               |
| ---------------   |:------------------:| ------------------:|
| Chrome            | 76+                | < 76               |
| Edge              | 79+                | < 79               |
| Firefox           | 67+                | < 67               |
| Opera             | 62+                | < 62               |
| Safari iOS        | 13+                | < 13               |
| Safari MacOS      | 12.1+              | < 12.1             |
| Android Webview   | 91+                | < 91               |
| Internet Explorer | NA                 | all                |

### Grey area browsers

Some browser versions exist in the grey area outside and/or between Enhanced and Core levels. For example:

* Old versions of an evergreen browser: a user has turned off auto-updates, or their upgrade opportunities are limited by their device or administrator.
* Nightly or developer versions of evergreen browsers.

We serve these grey area browsers the Enhanced version of a site, so they will receive the full experience. Due to resourcing implications we do not specifically test our products against them - however we do expect them to work (because, for example, [we strive to provide compatible CSS via Autoprefixer](#browserslist)). Over time, analysis of errors and usage patterns may cause some browsers in this grey area to be deliberately changed to either Enhanced or Core, to allow for better support.

## Implementing browser support

Our primary approach to classifying a browser support level is the "[Cutting the Mustard (CTM)](https://responsivenews.tumblr.com/post/18948466399/cutting-the-mustard)" progressive enhancement technique, based upon the principles developed by the BBC.

This approach works by using feature detection in order to determine which browsers will receive the full Enhanced experience (i.e. they "[cut the mustard](https://en.wiktionary.org/wiki/cut_the_mustard)") and which ones will receive only the Core experience.

### Implementation details

All browser versions load a basic stylesheet that contains only [normalisation](https://necolas.github.io/normalize.css/) and a few small enhancements to the user-agent stylesheet (typically max-width layout and colour and logo branding).

We then use CSS media queries to detect capable browsers. Unlike the approach described by the BBC, we don't use a JavaScript-based featured detection. We want users to have the best possible experience even if JavaScript is not available.

To load the full experience only in Enhanced browsers we implement logic in the media attribute of the `<link>` element that identifies the main stylesheet, loading the stylesheet only in browsers that recognise the properties of that media query:

```html
<link rel="stylesheet" href="enhanced.css" media="only print, only all and (prefers-color-scheme: no-preference), only all and (prefers-color-scheme: light), only all and (prefers-color-scheme: dark)" id="enhanced-stylesheet">
```

This technique is documented in [Cutting the Mustard with Media queries](https://www.sitepoint.com/cutting-the-mustard-with-css-media-queries/). The specific media queries we use are based upon [CSS Only Mustard Cut](https://github.com/Fall-Back/CSS-Mustard-Cut), with a preference towards combining them into one rather than separating them out into multiple `<link>` elements. Note that you **cannot** add line breaks to the media query if they are combined.

We couple the loading of JavaScript to the loading of the enhanced CSS. We use the [window.matchMedia](https://developer.mozilla.org/en/docs/Web/API/Window/matchMedia) API to detect when the browser loads the CSS within the media query. Once the enhanced CSS loads, this will cause the JavaScript code to load too.

```javascript
(function() {
  var linkEl = document.getElementById('enhanced-stylesheet');
  if (window.matchMedia && window.matchMedia(linkEl.media).matches) {
    var script = document.createElement('script');
    script.src = 'enhanced-script.js';
    script.async = true;
    document.body.appendChild(script);
  }
})();
```

### Caveats

#### Browsers without TLS 1.2 support

As of June 2018, all our sites are served through HTTPS using the [TLS 1.2 cryptographic protocol](https://en.wikipedia.org/wiki/Transport_Layer_Security#TLS_1.2) or newer. This means that users of browsers that don't support TLS 1.2 (e.g. Safari on iOS 4) will not be able to access our sites. Browsers that have support for TLS 1.2 not enabled by default (e.g. Internet Explorer on Windows 7) will not be able to access our sites, unless they change their default settings. We consider that this is required in order to keep our users secure.

The way that we restrict the connection to our sites when not using TLS 1.2 doesn't impact the way that we design and build our sites and our commitment to an approach based on progressive enhancement techniques.

#### .browserslist

While we do not test [grey-area browsers](#grey-area-browsers), we still work towards the best experience for all our users. CSS for grey-area browsers should therefore be prefixed using [Autoprefixer](https://github.com/postcss/autoprefixer). Automatically adding vendor prefixes allows us to increase support for these browsers with little extra effort.

The following `.browserslistrc` file ([a standard way of sharing target browser data](https://github.com/browserslist/browserslist)) should cover all browsers that receive Enhanced CSS according to our [Browser Support list](#browser-support-list).

```nanorc
defaults
ff > 66
chrome > 75
safari > 11
edge > 78
opera > 61
```
