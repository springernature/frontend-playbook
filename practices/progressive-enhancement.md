# Progressive enhancement

* [What is it?](#what-is-it)
* [Why we use it](#why-we-use-it)
* [Implementation](#implementation)
* [Common concerns](#common-concerns)
  * [Why do we care about those crusty old browsers? I'm building a ✨Web App✨, not a web page!](#why-do-we-care-about-those-crusty-old-browsers-im-building-a-✨web-app✨-not-a-web-page)
* [Find out more:](#find-out-more)

## What is it?

Progressive enhancement is a design and development practice that focuses on delivering the basic essentials of a website as a primary concern, then building the various layers of refinement and niceties on top of that for those clients than can receive them. In practice this means that we start with developing a logical and semantic HTML application with all the key functionality, then we can enhance this with an aesthetic layer (CSS) and behavioural layer (JavaScript) as desired.

There is a subtle but important difference in this approach vs the outdated approach of "graceful degradation" (or fault-tolerance) which it can often be confused with. Graceful degradation suggests a feature-complete "full-fat" application is designed and built, and is expected to be delivered wholesale to each client. Developers then attempt to build into the system fail safes so that when a client is unable to use the whole application, it can still get some value out of it.

## Why we use it

Progressive Enhancement fits perfectly with the [Rule of Least Power](https://en.wikipedia.org/wiki/Rule_of_least_power).

> In the web front-end stack — HTML, CSS, JS, and ARIA — if you can solve a problem with a simpler solution lower in the stack, you should. It’s less fragile, more foolproof, and just works.
>
> -- [Ian Featherstone, April 23rd 2014](https://simplyaccessible.com/article/data-attributes/)

By keeping the Rule of Least Power in mind you can create software that's fault tolerant by design - a key consideration for writing software for the web which will be downloaded and interpreted/executed in an incomprehensibly diverse plethora of devices and environments.

Unlike graceful degradation, this fault tolerance is built in *from the start* and so is much less likely to be skipped out in the interests of hitting a deadline (or because it's less spangly than the next feature X).

Developing software using progressive enhancement also encourages Lean thinking, by aligning development priorities with end-user priorities (people are likely here for your content, not for how pretty your buttons look). This is both very useful for prioritisation of features (and refinement of the fabled MVP) but also biases you towards delivery of software that can be tested early; so you can see if your core content and functionality is working before spending too much time on making it "cutting-edge".

Finally by starting with just the most basic layer of content and moving on from there, progressive enhancement encourages a lighter, more performant delivery of software. For someone on a slow network, or with a device which can't support the layers of sophistication you've built into your site, they'll appreciate being able to access the content and basic functionality you've provided even while the bells and whistles are downloaded/parsed/executed (or none of the above).

## Implementation

We enable progressive enhancement at every level of our products.

On the broadest level our [browser support](graded-browser-support.md) approach lets us offer Core versions of our products that work for all users, in all situations, and which are then enhanced when the browser is deemed advanced enough.

On the CSS level we build basic implementations first, using primitive CSS, and then enhance in Advanced browsers using the [cascade](https://developer.mozilla.org/en-US/docs/Web/CSS/Cascade), [specificity](https://developer.mozilla.org/en-US/docs/Web/CSS/Specificity), source order, and [feature queries](https://developer.mozilla.org/en-US/docs/Web/CSS/@supports).

With JavaScript we acknowledge that, given our [browser support chart](graded-browser-support.md#graded-browser-support-list), we must support ES5 browsers, which we do so via transpiling from ES6/Next to ES5. However we can then use [feature detection](https://developer.mozilla.org/en-US/docs/Learn/Tools_and_testing/Cross_browser_testing/Feature_detection) to offer more capabilities as the browser supports them.

## Common concerns

### Why do we care about those crusty old browsers? I'm building a ✨Web App✨, not a web page!

First of all; a web app is a web page, put your sparkles away. Secondly, why do you think it's only crusty old browsers who might not be able to render all of your bells and whistles? What about a shiny modern browser that has had its connection terminated before it downloaded your CSS/JS/other when its owners train plunged into a tunnel? Or what happens when one of your third-party advertising/analytics/other scripts causes a JavaScript exception that prevents further execution on the page? Progressive enhancement is not just a solution for clients with poor support for more modern technologies, it's also a failsafe for EVERY client which guarantees your site/application is as useful as it can be to everyone all the time.

### So you're saying I can't use JavaScript?

No, that's a misrepresentation of the purpose of progressive enhancement. There are many situations where you will _need_ to use JavaScript to achieve certain objectives. One example is the use of ARIA - you can't meaningfully use the `aria-expanded` property to indicate that a component progressively discloses information without JavaScript, because you need to be able to update the DOM depending on user activity. 

Use JavaScript defensively, on the assumption that there will frequently be times where it's not available. And since we're on the subject, [ARIA should be a progressive enhancement too](https://developer.paciellogroup.com/blog/2018/06/short-note-on-progressive-aria/). 


## Find out more

* [A List Apart: Understanding Progressive Enhancement](http://alistapart.com/article/understandingprogressiveenhancement) October 07, 2008
* [Progressive enhancement is a team sport](https://seesparkbox.com/foundry/Progressive_Enhancement_Is_A_Team_Sport)
* [Progressive enhancement is still important](https://jakearchibald.com/2013/progressive-enhancement-still-important/) July 03, 2013
* [Robustness and least power](https://adactio.com/journal/14327) September 10th, 2018
