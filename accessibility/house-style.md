# Accessibility style guide

This document outlines the way we make our sites accessible. It's a living styleguide – it will grow as our practices do.

- [General Principles](#general-principles)
  - [What is accessibility?](#what-is-accessibility)
  - [Why do we care about accessibility?](#why-do-we-care-about-accessibility)
- [VPATs](#vpats)
- [How we conform](#how-we-conform)
  - [Standards](#standards-we-conform-to)
  - [Tools and techniques](#tools-and-techniques)
    - [Guidelines](#guidelines)
    - [Pa11y](#pa11y)
    - [Other accessibility testing tools](#other-accessibility-testing-tools)
    - [Assistive technology](#assistive-technology)
    - [Testing with real users](#testing-with-real-users)
    - [Resources](#resources)


## General principles

> The power of the Web is in its universality.
> Access by everyone regardless of disability is an essential aspect.
>
> _Tim Berners-Lee, inventor of the World Wide Web_


### What is accessibility?

The Web is fundamentally designed to work for all people, whatever their hardware, software, language, culture, location, or physical or mental ability. When the Web meets this goal, it is accessible to people with a diverse range of hearing, movement, sight, and cognitive ability.

Thus the impact of disability is radically changed on the Web because the Web removes barriers to communication and interaction that many people face in the physical world. However, when websites, web technologies, or web tools are badly designed, they can create barriers that exclude people from using the Web.

It is essential that the Web be accessible in order to provide equal access and equal opportunity to people with diverse abilities. Indeed, the [UN Convention on the Rights of Persons with Disabilities](https://www.un.org/development/desa/disabilities/) recognises access to information and communications technologies, including the Web, as a basic human right.

Accessibility supports social inclusion for people with disabilities as well as others, such as older people, people in rural areas, and people in developing countries.


### Why do we care about accessibility?

- *It's a legal requirement:* we're legally obliged to make our content accessible to users with diverse needs. All of our websites MUST comply with [US Section 508](https://www.section508.gov/) of the US Rehabilitation Act 1973, [EU Directive 2016/2102](http://eur-lex.europa.eu/legal-content/EN/TXT/?uri=CELEX%3A32016L2102) and the [UK Equality Act 2010](http://www.legislation.gov.uk/ukpga/2010/15/contents). 
- *It makes financial sense:* around 20% of working age adults in the UK are estimated to have some kind of permanent disability (Source: [Scope UK](https://www.scope.org.uk/media/disability-facts-figures)). The Financial Times estimates that 26% of their users have a permanent disability (Source: [Laura Carvajal, JSConf](https://www.youtube.com/watch?v=H4FzW9oFObs)). Also taking into account people who are [temporarily disabled](https://userway.org/blog/how-situational-disabilities-impact-us-all), failing to make our websites accessible can cause a significant reduction in real market share. 
- *It's a technical requirement:* catering for all users complements our [browser support policy](../practices/graded-browser-support.md) (we aim to support all browsers), and our use of [progressive enhancement](../practices/progressive-enhancement.md). 
- *It's the right thing to do:* we have a duty to cater for all users regardless of ability. If we know that people can encounter difficulties accessing our content (which we do), and we know that we can do things to facilitate that access (which we do), then not making something accessible is knowingly contributing to the oppression of people with disabilities.

Accessible sites can be used by more people - including people with disabilities, people using mobile devices, older people, people with low literacy, people who are not fluent in the language of the site, people with low bandwidth connections to the Internet, people with older technologies, and new and infrequent web users.


## VPATs

A Voluntary Product Accessibility Template (VPAT) is a document which evaluates how accessible a particular product is [according to the Section 508 Standards](https://www.section508.gov/content/sell/vpat). 

A VPAT MUST be produced by you or your team for every product or service that we make commercially available in the United States. If something changes, e.g. accessibility is improved for a particular criteria, you MUST update the VPAT to reflect the change. 

You may use [our VPAT template](https://github.com/springernature/vpat) when creating this for your own products. 


## How we conform

### Standards we conform to

We aim to comply with [WCAG 1](https://www.w3.org/TR/WCAG10/) AA and the [WCAG Samurai Errata](http://www.wcagsamurai.org/erratas/introduction/). This gives us a high pass rate with [Web Content Accessibility Guidelines 2](https://www.w3.org/TR/WCAG20/) AA. 

Most Web sites that already conform to WCAG 1.0 do not require significant (or any) changes to conform to WCAG 2.0 (Source: [W3C WAI - How WCAG 2.0 Differs from WCAG 1.0](https://www.w3.org/WAI/WCAG20/from10/diff)). 

As of January 18th 2018, WCAG 2.0 AA will be incorporated into Section 508 (see [Section 508 Refresh Part 1](https://www.paciellogroup.com/blog/2017/01/section-508-refresh-part-1/) by the Paciello Group). 


### Tools and techniques

#### Guidelines

You are expected to be aware of the Web Content Accessibility Guidelines and to adhere to their recommendations. You are also expected to understand the foundational four principles of accessibility (Perceivable, Operable, Understandable, Robust) and to be able to apply them in your work. Be alert to the possibility of regressions that cannot be detected by software.

The companion document [Understanding WCAG 2.0](https://www.w3.org/TR/UNDERSTANDING-WCAG20/Overview.html) explains what each of the success criterion in WCAG 2.0 actually means. You might also find the [Techniques for WCAG 2.0](https://www.w3.org/TR/WCAG20-TECHS/) useful when building features. 

We've also created [a simple accessibility checklist](accessibility-checklist.md), to help you become familiar with the guidelines/standards, and to aid you when manually assessing pages.

Freely use [WAI-ARIA](https://www.w3.org/TR/wai-aria/) roles and properties in your code where they help to improve accessibility of your interfaces but you SHOULD NOT use aria techniques as a way of compensating for the abuse of semantics (e.g. do not apply `role="link"` to a `div` element, instead of using `a`, etc.)


#### Pa11y

We use [Pa11y](http://pa11y.org/) to perform automated accessibility testing. Projects MUST have Pa11y integrated at the build stage, and builds MUST fail if errors are introduced. You MUST NOT allow accessibility regressions to enter your project's codebase. 

Mature projects using Pa11y for the first time MAY use the `threshold` flag to specify a baseline number of errors to allow through, but MUST aim to reduce that threshold to zero at the earliest opportunity. Watch this talk by Laura Carvajal of the Financial Times to get a [high level overview of the concept](https://www.youtube.com/watch?v=H4FzW9oFObs). 

Read [Automated accessibility testing with Travis CI](http://cruft.io/posts/automated-accessibility-testing-node-travis-ci-pa11y/) to see how to integrate Pa11y with your build process. If you're not using Travis, adjust the setup for the software that you are using. 

*Caveat:* it's possible to build a site that passes Pa11y's testing with flying colours, but is still completely inaccessible for real users. You MUST NOT rely on Pa11y as your sole safeguard for accessibility testing. 


#### Other accessibility testing tools

- Pa11y is based on HTMLCodesniffer by Squizlabs. They also have a [bookmarklet](https://squizlabs.github.io/HTML_CodeSniffer/) for quick tests. 
- Google's Accessibility Developer Tools are available from the [Chrome Web Store](https://chrome.google.com/webstore/detail/accessibility-developer-t/fpkknkljclfencbdbgkenhalefipecmb?hl=en).
- WebAim's [WAVE toolbar](https://chrome.google.com/webstore/detail/wave-evaluation-tool/jbbplnpkjmmeebjpijfedlgcdilocofh) for Chrome evaluates accessibility in place on the page.
- Check colour contrast compliance with Jonathan Snook's [Colour Contrast Checker](https://snook.ca/technical/colour_contrast/colour.html#fg=33FF33,bg=333333).

*Caveat:* None of these tools on their own will catch every error. Even by combining all of them, it's still possible to produce an inaccessible webpage. Terrill Thompson [compared several of the most popular tools](http://terrillthompson.com/blog/730) which should give you some idea of the scale of the problem. You MUST NOT rely on accessibility tools as your sole safeguard for accessibility testing.


#### Assistive technology

You're encouraged to test your pages with assistive technology (AT). Many operating systems include some AT as standard, including screenreaders, magnifiers, or input remapping. 

In OSX you can enable [VoiceOver](https://support.apple.com/kb/PH22549?locale=en_US) in System Preferences > Accessibility. You may also find navigating without an input device using [Dictation](https://support.apple.com/en-us/HT202584) instructive. Ensure your interfaces work with keyboard navigation. 

*Caveat:* unless you're familiar with using AT, your experience won't be comparable to that of a habitual AT user. Beware of making inferences about what's "easier" for AT users based on your own preferences. 


#### Testing with real users

The best way to learn if your website works for people with disabilities is to get people with disabilities to test it for you. 

You can arrange your own user testing, but it's better to engage a third party like the [Digital Accessibility Centre](http://www.digitalaccessibilitycentre.org/) to do this work for you. As professionals who specialise in accessibility testing and making recommendations, they're better at it than you. 


#### Resources

Udacity have published an [excellent free course on Web Accessibility](https://www.udacity.com/course/web-accessibility--ud891) with Google engineers Alice Boxhall and Rob Dodson. 

The Financial Times have produced an [accessibility tip sheet](https://ft-interactive.github.io/accessibility/index.html).

