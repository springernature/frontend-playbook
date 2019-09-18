# Accessibility style guide

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

- *It's a legal requirement:* we're legally obliged to make our content accessible to users with diverse needs. All of our websites MUST comply with [US Section 508](https://www.section508.gov/) of the US Rehabilitation Act 1973, [EU Directive 2016/2102](http://eur-lex.europa.eu/legal-content/EN/TXT/?uri=CELEX%3A32016L2102) and the [UK Equality Act 2010](http://www.legislation.gov.uk/ukpga/2010/15/contents). From January 18th 2018, compliance with Section 508 requires us to comply with WCAG 2.0 AA. We expect this to be updated to WCAG 2.1 AA in due course.   
- *It makes financial sense:* around 20% of working age adults in the UK are estimated to have some kind of permanent disability (Source: [Scope UK](https://www.scope.org.uk/media/disability-facts-figures)). Forrester Research found that *_57%_* of computer users aged 18 to 64 have disabilities that make them "likely or very likely" to benefit from the use of assistive technology (Source: [Pubmed](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC2788505/)). Also taking into account people who are [temporarily disabled](https://userway.org/blog/how-situational-disabilities-impact-us-all), failing to make our websites accessible can cause a significant reduction in real market share. 
- *It's a technical requirement:* catering for all users complements our [browser support policy](../practices/graded-browser-support.md) (we aim to support all browsers), and our use of [progressive enhancement](../practices/progressive-enhancement.md). 
- *It's the right thing to do:* we have a duty to cater for all users regardless of ability. If we know that people can encounter difficulties accessing our content (which we do), and we know that we can do things to facilitate that access (which we do), then not making something accessible is knowingly contributing to the oppression of people with disabilities.

Accessible sites can be used by more people - including people with disabilities, people using mobile devices, older people, people with low literacy, people who are not fluent in the language of the site, people with low bandwidth connections to the Internet, people with older technologies, and new and infrequent web users.

![Microsoft illustration of how designing for permanent disabilities helps many people facing temporary or situational disability](images/microsoft-accessibility.jpg)

(image &copy; Microsoft)


## VPATs

A Voluntary Product Accessibility Template (VPAT) is a document that explains how accessible a particular product is [according to the Section 508 Standards](https://www.section508.gov/content/sell/vpat). Our customers in the United States use our VPATs to show that they comply with U.S. accessibility law. 

A VPAT MUST be produced by you or your team for every product or service that we make commercially available in the United States. If something changes, e.g. accessibility is improved for a particular criteria, you MUST update the VPAT to reflect the change. You MUST NOT regress accessibility to below the level detailed in the VPAT.

You may use [our VPAT template](https://github.com/springernature/vpat) when evaluating your own products. 


## How we conform

### Standards we aim for

Our target standards are [WCAG 2.1](https://www.w3.org/TR/WCAG21/) level AA.

As of mid-September 2018, WCAG 2.1 AA has been adopted in the European [EN 301 549 “Accessibility requirements for ICT products and services”](https://www.w3.org/blog/2018/09/wcag-2-1-adoption-in-europe/). This means that in order to comply with EN 301 549, your products MUST also comply with WCAG 2.1 to level AA.

As of January 18th 2018, WCAG 2.0 AA (the previous candidate recommendation) was incorporated by reference into Section 508 (see [Section 508 Refresh Part 1](https://www.paciellogroup.com/blog/2017/01/section-508-refresh-part-1/) by the Paciello Group). 

Our expectation is that Section 508 will be updated to reference WCAG 2.1 in due course. Comply with WCAG 2.1 now to avoid retrofitting repairs later!  


### Tools and techniques

#### Guidelines

You are expected to be aware of the Web Content Accessibility Guidelines and to adhere to their recommendations. You are also expected to understand the foundational four principles of accessibility (Perceivable, Operable, Understandable, Robust) and to be able to apply them in your work. Be alert to the possibility of regressions that cannot be detected by software.

The companion document [Understanding WCAG 2.1](https://www.w3.org/WAI/WCAG21/Understanding/) (Editor's Draft) explains what each of the success criterion in WCAG 2.1 actually means. You might also find the [Techniques for WCAG 2.1](https://www.w3.org/WAI/WCAG21/Techniques/) (Editor's Draft) useful when building features. 

W3C WAI have published a [quick reference document for WCAG](https://www.w3.org/WAI/WCAG21/quickref/?versions=2.0). It describes the WCAG success criteria and shows techniques and failures for each. We've also created [a simple accessibility checklist](accessibility-checklist.md), to help you become familiar with the guidelines/standards, and to aid you when manually assessing pages. 

Use [WAI-ARIA](https://www.w3.org/TR/wai-aria/) roles and properties in your code where they help to improve accessibility of your interfaces but you SHOULD NOT: 
* Use ARIA techniques as a way of compensating for the abuse of semantics (e.g. do not apply `role="link"` to a `div` element, instead of using `a`, etc.);
* Use ARIA roles, properties, or design patterns without understanding what they do;
* Use ARIA roles, properties, or design patterns without testing them with assistive technologies.

The W3C [Using ARIA](https://www.w3.org/TR/using-aria/#NOTES) working draft explains why you shouldn't do those things. Familiarise yourself in particular with the First and Second Rules of ARIA! 


#### Pa11y

We use [Pa11y](http://pa11y.org/) to perform automated accessibility testing. Projects MUST have Pa11y integrated at the build stage, and builds MUST fail if errors are introduced. You MUST NOT allow accessibility regressions to enter your project's codebase. 

Mature projects using Pa11y for the first time MAY use the `threshold` flag to specify a baseline number of errors to allow through, but MUST aim to reduce that threshold to zero at the earliest opportunity. [Watch this talk by Laura Carvajal of the Financial Times](https://www.youtube.com/watch?v=H4FzW9oFObs) to get a high level overview of the concept. 

Read [Automated accessibility testing with Travis CI](http://cruft.io/posts/automated-accessibility-testing-node-travis-ci-pa11y/) to see how to integrate Pa11y with your build process. If you're not using Travis, adjust the setup for the software that you are using. 

*Caveat:* it's possible to build a site that passes Pa11y's testing with flying colours, but is still completely inaccessible for real users. You MUST NOT rely on Pa11y as your sole safeguard for accessibility testing. 


#### Other accessibility testing tools

- Pa11y is based on HTMLCodesniffer by Squizlabs. They also have a [bookmarklet](https://squizlabs.github.io/HTML_CodeSniffer/) for quick tests. 
- The Axe engine comes as a [browser extension](https://www.deque.com/axe/) and as an [NPM module](https://github.com/dequelabs/axe-core) that you can integrate with your build, like Pa11y. 
- Google's [Lighthouse](https://developers.google.com/web/tools/lighthouse/) audits accessibility as well as other metrics (e.g. performance) and is available as an extension, in the Chrome dev console, or as a Node CLI tool. 
- WebAim's [WAVE extension](https://wave.webaim.org/extension/) for Chrome and Firefox evaluates accessibility in place on the page. 
- Check colour contrast compliance with WebAim's [Colour Contrast Checker](https://webaim.org/resources/contrastchecker/).
- The [Landmarks browser extension](http://matatk.agrip.org.uk/landmarks/) (for Firefox, Chrome and Opera) enables navigation of WAI-ARIA landmarks, via the keyboard or a pop-up menu.
- [Funkify](http://www.funkify.org/) is an extension for Chrome that helps you experience the web and interfaces through the eyes of users with different abilities and disabilities.

*Caveat:* None of these tools on their own will catch every error. Even by combining all of them, it's still possible to produce an inaccessible webpage. Terrill Thompson [compared several of the most popular tools](http://terrillthompson.com/blog/730) which should give you some idea of the scale of the problem. The Government Digital Service also [conducted their own tool audit](https://accessibility.blog.gov.uk/2017/02/24/what-we-found-when-we-tested-tools-on-the-worlds-least-accessible-webpage/). 

You MUST NOT rely on accessibility tools as your sole safeguard for accessibility testing.


#### Assistive technology

You're encouraged to test your pages with assistive technology (AT). Many operating systems include some AT as standard, including screenreaders, magnifiers, or input remapping. 

In OSX you can enable [VoiceOver](https://help.apple.com/voiceover/info/guide/10.12/#/) in System Preferences > Accessibility. You may also find navigating without an input device using [Dictation](https://support.apple.com/en-us/HT202584) instructive. Ensure your interfaces work with keyboard navigation. 

*Caveat:* unless you're familiar with using AT, your experience won't be comparable to that of a habitual AT user. Beware of making inferences about what's "easier" for AT users based on your own preferences. 


#### Testing with real users

The best way to learn if your website works for people with disabilities is to get people with disabilities to test it for you. 

You can arrange your own user testing, but it's better to engage a third party like the [Digital Accessibility Centre](http://www.digitalaccessibilitycentre.org/) to do this work for you. As professionals who specialise in accessibility testing and making recommendations, they're better at it than you. 


#### Resources

Udacity have published an [excellent free course on Web Accessibility](https://www.udacity.com/course/web-accessibility--ud891) with Google engineers Alice Boxhall and Rob Dodson. 

The Financial Times have produced an [accessibility tip sheet](https://ft-interactive.github.io/accessibility/index.html).

The Government Digital Service frequently publishes excellent resources. Some highlights are:

* [We're making accessibility clearer and easier](https://gds.blog.gov.uk/2017/10/23/were-making-accessibility-clearer-and-easier/)
* [Making your service accessible: an introduction](https://www.gov.uk/service-manual/helping-people-to-use-your-service/making-your-service-accessible-an-introduction)

