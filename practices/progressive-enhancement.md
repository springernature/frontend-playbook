# Progressive enhancement

* [What is it?](#what-is-it)
* [Why we use it](#why-we-use-it)
* [Implementation](#implementation)
* [Common concerns](#common-concerns)
  * [How many users turn JavaScript off, anyway?](#how-many-users-turn-javascript-off-anyway)
  * [OK, so how often does JavaScript fail? How can we test for that?](#ok-so-how-often-does-JavaScript-fail-how-can-we-test-for-that)
  * [So you're saying I can't use JavaScript?](#so-youre-saying-i-cant-use-javascript)
* [Find out more:](#find-out-more)

## What is it?

Progressive enhancement is a design and development practice that focuses on delivering the basic essentials of a website as a primary concern, then building the various layers of refinement and niceties on top of that for those clients than can receive them. In practice this means that we start with developing a logical and semantic HTML application with all the key functionality, then we can enhance this with an aesthetic layer (CSS) and behavioural layer (JavaScript) as desired.

There is a subtle but important difference in this approach vs the outdated approach of "graceful degradation" (or fault-tolerance) which it can often be confused with. Graceful degradation suggests a feature-complete "full-fat" application is designed and built, and is expected to be delivered wholesale to each client. Developers then attempt to build into the system fail safes so that when a client is unable to use the whole application, it can still get some value out of it.

## Why we use it

Progressive Enhancement fits perfectly with the [Rule of Least Power](https://en.wikipedia.org/wiki/Rule_of_least_power).

> In the web front-end stack — HTML, CSS, JS, and ARIA — if you can solve a problem with a simpler solution lower in the stack, you should. It’s less fragile, more foolproof, and just works.
>
> -- [Derek Featherstone, April 23rd 2014](https://simplyaccessible.com/article/data-attributes/)

By keeping the Rule of Least Power in mind you can create software that's fault tolerant by design - a key consideration for writing software for the web which will be downloaded and interpreted/executed in an incomprehensibly diverse plethora of devices and environments.

Unlike graceful degradation, this fault tolerance is built in *from the start* and so is much less likely to be skipped out in the interests of hitting a deadline (or because it's less spangly than the next feature X).

Developing software using progressive enhancement also encourages Lean thinking, by aligning development priorities with end-user priorities (people are likely here for your content, not for how pretty your buttons look). This is both very useful for prioritisation of features (and refinement of the fabled MVP) but also biases you towards delivery of software that can be tested early; so you can see if your core content and functionality is working before spending too much time on making it "cutting-edge".

Finally by starting with just the most basic layer of content and moving on from there, progressive enhancement encourages a lighter, more performant delivery of software. For someone on a slow network, or with a device which can't support the layers of sophistication you've built into your site, they'll appreciate being able to access the content and basic functionality you've provided even while the bells and whistles are downloaded/parsed/executed (or none of the above).

## Implementation

We enable progressive enhancement at every level of our products.

On the broadest level our [browser support](graded-browser-support.md) approach lets us offer Core versions of our products that work for all users, in all situations, and which are then enhanced when the browser is deemed advanced enough.

On the CSS level we build basic implementations first, using primitive CSS, and then enhance in more advanced browsers using the [cascade](https://developer.mozilla.org/en-US/docs/Web/CSS/Cascade), [specificity](https://developer.mozilla.org/en-US/docs/Web/CSS/Specificity), source order, and [feature queries](https://developer.mozilla.org/en-US/docs/Web/CSS/@supports).

With JavaScript we acknowledge that, given our [browser support chart](graded-browser-support.md#graded-browser-support-list), we must support ES5 browsers, which we do so via transpiling from ES6/Next to ES5. However we can then use [feature detection](https://developer.mozilla.org/en-US/docs/Learn/Tools_and_testing/Cross_browser_testing/Feature_detection) to offer more capabilities as the browser supports them.

## Common concerns

### How many users turn JavaScript off anyway?

Not very many, but this usually isn't the question you really need to be asking. A more useful, subtly different, question is "how many users don't have JavaScript available?" The reasons for JavaScript delivery failure are varied. In 2015, Stuart Langridge published an ["Everyone has JavaScript, right?" flowchart](https://www.kryogenix.org/code/browser/everyonehasjs.html). The web is a fast-moving environment, but as of writing in 2023, everything on the flowchart is still relevant. All users will have times when JavaScript fails, for all kinds of reasons, and mostly they're not in control of why and when it happens. The active choice to turn JavaScript off (which people still do), is fairly far down the list of reasons for not having working JavaScript.

Progressive enhancement is not just a solution for clients who have deliberately deprived themselves of JavaScript, it's also a failsafe for EVERY client which guarantees your site/application is as useful as it can be to everyone all the time.

### OK, so how often does JavaScript fail? How can we test for that?

Usually this question comes from the Extreme Programming thinking of "[You Ain't Gonna Need It](https://en.wikipedia.org/wiki/You_aren%27t_gonna_need_it)" - the desire to only implement features when they're necessary. However, as the previous section ("How many users turn JavaScript off anyway?") makes clear, JavaScript delivery failure happens to everyone, some of the time. Robustness is a core requirement for our websites and applications, not an optional feature. Stuart Langridge illustrates why you need to think in terms of [JavaScript failing for a % of _visits_, not _users_](https://www.kryogenix.org/code/browser/why-availability/).

At this stage, you may be wondering why I've not answered the question directly. How many, exactly? That's because it's hard to test for - if there's no JavaScript, there's no tracking. For this reason, not very many people have tried it. Those who do include [Yahoo! back in 2010](https://web.archive.org/web/20130622121741/https://developer.yahoo.com/blogs/ydn/many-users-JavaScript-disabled-14121.html), and [the UK Government Digital Service in 2013](https://gds.blog.gov.uk/2013/10/21/how-many-people-are-missing-out-on-javascript-enhancement/). These groups found a failure rate of about 1.1% to 1.3% of requests. Again, this is across all users and devices, of all capacities and capabilities, not just "people who turned JavaScript off", or "people using old browsers".

### So you're saying I can't use JavaScript?

No, that's a misrepresentation of the purpose of progressive enhancement. There are many situations where you will _need_ to use JavaScript to achieve certain objectives. One example is the use of ARIA - you can't meaningfully use the `aria-expanded` property to indicate that a component progressively discloses information without JavaScript, because you need to be able to update the DOM depending on user activity.

Use JavaScript defensively, on the assumption that there will frequently be times where it's not available. And since we're on the subject, [ARIA should be a progressive enhancement too](https://developer.paciellogroup.com/blog/2018/06/short-note-on-progressive-aria/).


## Find out more

* [A List Apart: Understanding Progressive Enhancement](http://alistapart.com/article/understandingprogressiveenhancement) October 07, 2008
* [Progressive enhancement is a team sport](https://seesparkbox.com/foundry/Progressive_Enhancement_Is_A_Team_Sport)
* [Progressive enhancement is still important](https://jakearchibald.com/2013/progressive-enhancement-still-important/) July 03, 2013
* [Robustness and least power](https://adactio.com/journal/14327) September 10th, 2018
