# Accessibility tools

- [Automated testing](#automated-testing)
  - [Pa11y and axe](#pa11y-and-axe)
- [Manual testing](#manual-testing)
- [Assistive technology](#assistive-technology)
- [Other accessibility tools](#other-accessibility-tools)
  - [Accessibility testing tools in the browser](accessibility-testing-tools-in-the-browser)
  - [Tools for manually analysing web pages](tools-for-manually-analysing-web-pages)
- [Simulators](#simulators)

## Automated testing

Automated accessibility testing can be used to detect the most common accessibility problems. This is only the first step in the process; you MUST NOT rely on automated testing as your sole method of verification! 

The GDS Accessibility team ran an experiment in 2017 to [audit the performance of a large number of available automated accessibility testing tools](https://accessibility.blog.gov.uk/2017/02/24/what-we-found-when-we-tested-tools-on-the-worlds-least-accessible-webpage/). They found that the highest number of errors that one tool was able to detect was 40%. The majority of the tools fell into the 20%-30% range. 


### Pa11y and axe

We use [Pa11y](http://pa11y.org/) to perform automated accessibility testing. Pa11y is an automated accessibility testing tool that supports [HTML_Codesniffer](https://squizlabs.github.io/HTML_CodeSniffer/) by Squizlabs, and [axe](https://www.deque.com/axe/) by Deque. 

Projects MUST have Pa11y integrated at the build stage, and builds MUST fail if errors are introduced. You MUST NOT allow accessibility regressions to enter your project's codebase. 

Mature projects using Pa11y for the first time MAY use the `threshold` flag to specify a baseline number of errors to allow through, but MUST aim to reduce that threshold to zero at the earliest opportunity. [Watch this talk by Laura Carvajal of the Financial Times](https://www.youtube.com/watch?v=H4FzW9oFObs) to get a high level overview of the concept. 

Read [Automated accessibility testing with Travis CI](http://cruft.io/posts/automated-accessibility-testing-node-travis-ci-pa11y/) to see how to integrate Pa11y with your build process. If you're not using Travis, adjust the setup for the software that you are using. 

You can use HTML_Codesniffer or axe as your test suite; we recommend using both. Neither engine is "better" than the other, they just use different testing strategies. When you fail builds based on Pa11y results, bear in mind that the two engines return different numbers of results, and that the results are formatted differently. 

When using axe, you may prefer to use the standalone [NPM module](https://github.com/dequelabs/axe-core) directly, instead of wrapping it with Pa11y. 


## Manual testing


## Assistive technology


## Other accessibility tools

### Accessibility testing tools in the browser

- Squizlabs also have an [HMTML_Codesniffer bookmarklet](https://squizlabs.github.io/HTML_CodeSniffer/) for quick tests. 
- The Axe engine comes as a [browser extension](https://www.deque.com/axe/) and as an [NPM module](https://github.com/dequelabs/axe-core) that you can integrate with your build, like Pa11y. 
- WebAim's [WAVE extension](https://wave.webaim.org/extension/) for Chrome and Firefox evaluates accessibility in place on the page. 
- Google's [Lighthouse](https://developers.google.com/web/tools/lighthouse/) audits accessibility as well as other metrics (e.g. performance) and is available as an extension, in the Chrome dev console, or as a Node CLI tool. 


### Tools for manually analysing web pages

- Check colour contrast compliance with WebAim's [Colour Contrast Checker](https://webaim.org/resources/contrastchecker/).
- The [Landmarks browser extension](http://matatk.agrip.org.uk/landmarks/) (for Firefox, Chrome and Opera) enables navigation of WAI-ARIA landmarks, via the keyboard or a pop-up menu.


## Simulators


