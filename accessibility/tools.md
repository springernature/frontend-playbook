# Accessibility tools

- [Automated testing](#automated-testing)
  - [Pa11y and axe](#pa11y-and-axe)
- [Manual testing](#manual-testing)
- [Assistive technology](#assistive-technology)
  - [Screen readers](#screen-readers)
- [Other accessibility tools](#other-accessibility-tools)
  - [Accessibility testing tools in the browser](#accessibility-testing-tools-in-the-browser)
  - [Tools for manually analysing web pages](#tools-for-manually-analysing-web-pages)
- [Simulators](#simulators)

## Automated testing

Automated accessibility testing can be used to detect the most common accessibility problems. This is only the first step in the process; you MUST NOT rely on automated testing as your sole method of verification! 

The GDS Accessibility team ran an experiment in 2017 to [audit the performance of a large number of available automated accessibility testing tools](https://accessibility.blog.gov.uk/2017/02/24/what-we-found-when-we-tested-tools-on-the-worlds-least-accessible-webpage/). They found that the highest number of errors that one tool was able to detect was 40%. The majority of the tools fell into the 20%-30% range. 


### Pa11y and axe

We use [Pa11y](http://pa11y.org/) to perform automated accessibility testing. Pa11y is an automated accessibility testing tool that supports [HTML_Codesniffer](https://squizlabs.github.io/HTML_CodeSniffer/) by Squizlabs, and [axe](https://www.deque.com/axe/) by Deque. 

Projects MUST have Pa11y integrated at the build stage, and builds MUST fail if errors are introduced. You MUST NOT allow accessibility regressions to enter your project's codebase. We're aiming to make accessibility better, so our baseline is to not make it worse. 

Mature projects using Pa11y for the first time MAY use the `threshold` flag to specify a baseline number of errors to allow through, but MUST aim to reduce that threshold to zero at the earliest opportunity. [Watch this talk by Laura Carvajal of the Financial Times](https://www.youtube.com/watch?v=H4FzW9oFObs) to get a high level overview of the concept. 

Read [Automated accessibility testing with Travis CI](http://cruft.io/posts/automated-accessibility-testing-node-travis-ci-pa11y/) to see how to integrate Pa11y with your build process. If you're not using Travis, adjust the setup for the software that you are using. 

You can use HTML_Codesniffer or axe as your test suite; we recommend using both. Neither engine is "better" than the other, they just use different testing strategies. When you fail builds based on Pa11y results, bear in mind that the two engines return different numbers of results, and that the results are formatted differently. 

When using axe, you may prefer to use the standalone [NPM module](https://github.com/dequelabs/axe-core) directly, instead of wrapping it with Pa11y. 


## Manual testing

Manual accessibility testing fills in the gaps that automated tools miss. 

- Microsoft’s [free Accessibility Insights tool](https://accessibilityinsights.io/) is a browser extension for Chrome that will guide you through the process of assessing a webpage for basic accessibility compliance. 


## Assistive technology

You're encouraged to test your pages with assistive technology (AT). Many operating systems include some AT as standard, including screenreaders, magnifiers, or input remapping. 

Make sure you test your work at high magnification. You may also find navigating without an input device using [Voice Control](https://support.apple.com/en-au/HT210539) instructive. Ensure your interfaces work with keyboard navigation. 

Unless you're familiar with using AT, your experience won't be comparable to that of a habitual AT user. Beware of making inferences about what's "easier" for AT users based on your own preferences. 

### Screen readers

If you don’t use a screen reader regularly, the way that you use it will be different to that of a habitual screen reader user, so be cautious in extrapolating your own experiences to those of other users. But also bear in mind that not all regular screen reader users are experts or power users, just like not all users of web browsers are experts. 

If you’re a Mac user, VoiceOver is built-in to OSX and is a decent, basic screen reader. This guide from WebAIM [explains the basics of using VoiceOver to test pages](https://webaim.org/articles/voiceover/). 

If you’re a Windows user, NVDA is one of the more popular screen readers amongst blind users. This guide from WebAIM [explains the basics of using NVDA to test pages](https://webaim.org/articles/nvda/).

On mobile, VoiceOver is built-in on iOS devices, and TalkBack is usually built-in on Android devices. 71% of respondents to the [WebAIM Screen Reader User Survey #8](https://webaim.org/projects/screenreadersurvey8/#mobilescreenreaders) use iOS VoiceOver on mobile. 

## Other accessibility tools

None of these tools on their own will catch every error. Even by combining all of them, it's still possible to produce an inaccessible webpage. Terrill Thompson [compared several of the most popular tools](http://terrillthompson.com/blog/730) which should give you some idea of the scale of the problem. The Government Digital Service also [conducted their own tool audit](https://accessibility.blog.gov.uk/2017/02/24/what-we-found-when-we-tested-tools-on-the-worlds-least-accessible-webpage/). 

You MUST NOT rely on these accessibility tools as your sole safeguard for accessibility testing.


### Accessibility testing tools in the browser

- Squizlabs also have an [HMTML_Codesniffer bookmarklet](https://squizlabs.github.io/HTML_CodeSniffer/) for quick tests. 
- The Axe engine comes as a [browser extension](https://www.deque.com/axe/) and as an [NPM module](https://github.com/dequelabs/axe-core) that you can integrate with your build, like Pa11y. 
- WebAim's [WAVE extension](https://wave.webaim.org/extension/) for Chrome and Firefox evaluates accessibility in place on the page. 
- Google's [Lighthouse](https://developers.google.com/web/tools/lighthouse/) audits accessibility as well as other metrics (e.g. performance) and is available as an extension, in the Chrome dev console, or as a Node CLI tool. 


### Tools for manually analysing web pages

- Check colour contrast compliance with WebAim's [Colour Contrast Checker](https://webaim.org/resources/contrastchecker/).
- The [Landmarks browser extension](http://matatk.agrip.org.uk/landmarks/) (for Firefox, Chrome and Opera) enables navigation of WAI-ARIA landmarks, via the keyboard or a pop-up menu.


## Simulators

Disability simulators are apps, extensions, or experiments that imitate the experience of being disabled for able-bodied people. They're designed to increase empathy and awareness of the issues facing disabled people. 

It's very important that you understand the limitations of disability simulators. No browser extension could ever give you an appreciation of what it's like to navigate the world as a disabled person. No blindfold game can teach you what it's like to be systematically discriminated against in virtually every aspect of your daily life. You can just switch the simulator off - a 
disabled person doesn't have that option. 

If used carelessly, disability simulators can also have the opposite effect of what's intended. Instead of giving able-bodied people empathy with those who experience disability in a particular context, they can elicit sympathy or pity reactions. Pity reactions lead to responses like "that's terrible", and not "how can we help?". As web professionals who care about the experiences of all of our users, we need to make sure our response to any disability simulators is "how can we help?". The [June 2017 issue of Braille Monitor](https://www.nfb.org/images/nfb/publications/bm/bm17/bm1706/bm170602.htm) discusses the research on disability simulation, its limitations, and how it can be improved. 

With this caveat in mind, here are some disability simulators that _may_ help you or your team understand _some_ of the ways in which people with some disabilities may perceive your web pages. 

- [Funkify](http://www.funkify.org/) is an extension for Chrome that helps you experience the web and interfaces through the eyes of users with different abilities and disabilities.
- [Empathy prompts](https://empathyprompts.net/) are flashcards with things to consider when making things for others to use.
