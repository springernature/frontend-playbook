# Graded Browser Support


## Our criteria for browser support


We follow the guidelines for graded browser support outlined by Nate Koechley at Yahoo:
[Yahoo Grade Browser Support guide](https://github.com/yui/yui3/wiki/Graded-Browser-Support)



| Tables        | Grade-A support | Grade-C support  |
| ------------- |:---------------:| ----------------:|
| Chrome        | latest stable   |                  |
| Edge          | latest stable   |                  |
| Firefox       | latest stable   |               $1 |
| IE            | 9, 10, 11       |               <9 |
| Opera         | latest stable   |              <10 |
| Safari        | latest stable, latest stable -1   |  <4.1 (desktop) |
| Webkit        | Android 4.&#8224; |  <3           |





## How we implement graded browser support


There are currently two methods by which implement graded support for browsers using principles of progressive enhancement.

In some instances we use user-agent sniffing to determine if a users browser falls into our pre-determined group of grade-c browsers, in which case we serve only the basic stylesheet and exclude the full experience.


In other cases where querying the user agent is not feasible we apply a 'cutting the mustard' approach to graded browser support, based upon the principles developed by the BBC: [Cutting the Mustard](http://responsivenews.co.uk/post/18948466399/cutting-the-mustard)

We load our basic stylesheet to all users. This contains only normalisation and a few small enhancements to the user-agent stylesheet. To load the full experience only in modern browsers we implement logic in the media attribute of the link element that identifies the main stylesheet, loading the stylesheet only in browsers that recognise the properties of that media query. The technique is documented here: [Cutting the Mustard with Media queries](https://www.sitepoint.com/cutting-the-mustard-with-css-media-queries/).

We use the following link attribute to conditionally load our main css:

```html
<link href="style.css" rel="stylesheet"  media="only screen and (-webkit-min-device-pixel-ratio:0), (min-color-index:0), (-ms-high-contrast: none)" />

```

We initialise JavaScript only if the browser supports a number of modern features:


```javascript
if ('querySelector' in document && 'localStorage' in window && 'addEventListener' in window) {
     // bootstrap the javascript application
}
```
