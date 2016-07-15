# Progressive Enhancement

## What is progressive enhancement

Progressive enhancement is a design and development practice that focuses on delivering the basic essentials of a website as a primary concern, then building the various layers of refinement and niceties on top of that for those clients than can receive them.  In practice this means that we start with developing a logical and semantic HTML application with all the key functionality, then we can enhance this with an aesthetic layer (CSS) and behavioural layer (JavaScript) as desired.

There is a subtle but important difference in this approach vs the approach of "graceful degradation" (or fault-tolerance) which it can often be confused with.  Graceful degradation suggests a feature-complete "full-fat" application is designed and built, and is expected to be delivered wholesale to each client.  Developers then attempt to build into the system fail safes so that when a client is unable to use the whole application, it can still get some value out of it.

## Why we use progressive enhancement

There are several key benefits to using progressive enhancement;

It allows you to create software that's fault tolerant by design - a key consideration for writing software for the web which will be downloaded and interpreted/executed in an incomprehensibly diverse plethora of devices and environments.  Unlike graceful degradation, this fault tolerance is built in *from the start* and so is much less likely to be skipped out because it's less sexy than the next feature X or in the interests of hitting a deadline.

Developing software using progressive enhancement also encourages Lean thinking, by aligning development priorities with end-user priorities (people are likely here for your content, not for how pretty your buttons look).  This is both very useful for prioritisation of features (and refinement of the fabled MVP) but also biases you towards delivery of software that can be tested early; so you can see if your core content and functionality is working before spending too much time on making it "cutting-edge".

Finally by starting with just the most basic layer of content and moving on from there, progressive enhancement encourages a lighter, more performant delivery of software.  For someone on a slow network, or with a device which can't support the layers of sophistication you've built into your site, they'll appreciate being able to access the content and basic functionality you've provided even while the bells and whistles are downloaded/parsed/executed (or none of the above).

## Common concerns

### Why do we care about those crusty old browsers?  I'm building a ✨Web App✨, not a web page!

First of all; a web app is a web page, put your sparkles away.  Secondly, why do you think it's only crusty old browsers who might not be able to render all of your bells and whistles?  What about a shiny modern browser that has had its connection terminated before it downloaded your CSS/JS/other when its owners train plunged into a tunnel?  Or what happens when one of your third-party advertising/analytics/other scripts causes a JavaScript exception that prevents further execution on the page?  Progressive enhancement is not just a solution for clients with poor support for more modern technologies, it's also a failsafe for EVERY client which guarantees your site/application is as useful as it can be to everyone all the time.

## Find out more:

* [A List Apart: Understanding Progressive Enhancement](http://alistapart.com/article/understandingprogressiveenhancement) October 07, 2008
* [Progressive enhancement is still important](https://jakearchibald.com/2013/progressive-enhancement-still-important/) July 03, 2013
