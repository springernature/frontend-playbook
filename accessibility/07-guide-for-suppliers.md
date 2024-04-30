# Developing accessible products

Businesses with an online presence must ensure they make their offering accessible to disabled users. This is a legal obligation that we are required to meet in multiple countries and jurisdictions. 

Certain organisations such as scientific or educational institutions may be prevented by various regulations from procuring products and services that do not meet accessibility requirements. Such regulations include (but are not limited to): 

* [Directive (EU) 2016/2102](https://eur-lex.europa.eu/legal-content/EN/TXT/?uri=CELEX%3A32016L2102) of the European Parliament.
* [Section 508](https://www.section508.gov/) in the US.
* The [Public Sector Bodies (Websites and Mobile Applications) (No. 2) Accessibility Regulations 2018](https://www.legislation.gov.uk/uksi/2018/952/contents/made) in the UK.

Commercial products are generally covered under civil rights legislation such as:

* The [Americans with Disabilities Act](https://www.ada.gov/) in the US.
* The [Equality Act 2010](https://www.legislation.gov.uk/ukpga/2010/15/contents) in the UK.
* Regulation instituted in EU member states as a consequence of the [European Accessibility Act](https://eur-lex.europa.eu/legal-content/EN/TXT/?uri=CELEX%3A32019L0882). 

If a commercial website is found to be inaccessible, the website owner can be sued for discrimination under various civil rights legislatory mechanisms.


## What is WCAG?

[The Web Content Accessibility Guidelines (WCAG)](https://www.w3.org/TR/WCAG21/) are a set of recommendations for making Web content more accessible to a wider range of people with disabilities. The guidelines address accessibility of web content on desktops, laptops, tablets, and mobile devices. Following these guidelines will also often make Web content more usable to users in general.

Several legal jurisdictions, including those in the US and the EU, explicitly refer to WCAG as the standard to which website operators are expected to adhere. 

Our target standard is WCAG 2.1 AA, in line with the current EU legislation, EN 301 549. *All first and third party web products and components published by Springer Nature must conform to WCAG 2.1 AA.* 


## How do I make sure my product complies?

Accessibility should be considered at every stage of your design and build process, not scheduled as a single clean-up task at the end of the project. Retrofitting accessibility into an inaccessible product is difficult, expensive, and time-consuming. 


### Accessible design patterns

When creating interactive components, look for an accessible design pattern before trying to roll your own. There are many resources where you can get ideas: 

* [https://a11yproject.com/patterns](https://a11yproject.com/patterns) 
* [https://www.w3.org/WAI/tutorials/](https://www.w3.org/WAI/tutorials/) 
* [https://inclusive-components.design/](https://inclusive-components.design/) 
* [https://design-system.service.gov.uk/components/](https://design-system.service.gov.uk/components/) 
* [https://www.w3.org/TR/wai-aria-practices-1.1/#aria_ex](https://www.w3.org/TR/wai-aria-practices-1.1/#aria_ex) 

You should still be cautious when using these design patterns. A particular design pattern may be aspirational, and untested with a wide range of Assistive Technology. You must test any “accessible” component that you incorporate to make sure it lives up to its claims. 

Before handing off your product for review, you should do the following:


### Automated testing

Automated accessibility testing can be used to detect the most common accessibility problems. This is only the first step in the process; you must not rely on automated testing as your sole method of verification. The GDS Accessibility team ran an experiment in 2017 to [audit the performance of a large number of available automated accessibility testing tools](https://accessibility.blog.gov.uk/2017/02/24/what-we-found-when-we-tested-tools-on-the-worlds-least-accessible-webpage/). They found that the highest number of errors that one tool was able to detect was 40%. The majority of the tools fell into the 20%-30% range. 

At Springer Nature, we use [Pa11y](http://pa11y.org/). It incorporates the [Axe](https://www.deque.com/axe/) and [HTML_CodeSniffer](https://squizlabs.github.io/HTML_CodeSniffer/) automated accessibility testing engines. Pa11y can be installed as part of your Continuous Integration setup if you’re using one, or can otherwise be used on the command line. Axe and HTML_CodeSniffer can also be used in the browser. 

We expect your product to be free of errors when passed through Pa11y. You’re welcome to use [other automated accessibility testing tools](https://github.com/springernature/frontend-playbook/blob/main/accessibility/01-popular-tools.md#other-accessibility-tools) in addition. 

You should also check your HTML is valid before handing off your work - you can use a service like the [WC3 validator](https://validator.w3.org/) or a browser extension. As well as reducing cross-browser bugs, this will catch some common accessibility errors.


### Manual testing

Manual accessibility testing fills in the gaps that automated tools miss. 


#### Guided tests

As a first step for manual testing, we recommend using Microsoft’s [free Accessibility Insights tool](https://accessibilityinsights.io/), a browser extension for Chrome. This tool will guide you through the process of assessing a webpage for basic accessibility compliance. It includes (but is not limited to) tests for:

* Unacceptably low contrast
* Missing alternative text on images
* Missing form labels
* Lack of keyboard navigability
* Lack of captions, audio descriptions, or alternatives to rich media
* Lack of visible focus styles

Use the “Assessment” functionality for this test. The “Fast Pass” function is included as part of the “Assessment” process. 

The Fast Pass functionality is based on Axe, but bear in mind that the bundled Axe version may not be in sync with the official package, and you may get inconsistent results if you rely on the version bundled by Microsoft. 

We expect your product to be free of errors that can be identified using this tool. 


#### Testing with a screen reader

The Accessibility Insights tool doesn’t cover screen reader testing. We do expect products to be usable in screen readers, so you should conduct your own testing with at least one of these. 

You will need to learn how to use a screen reader, but they are not complicated tools. They are consumer software products, designed to allow ordinary users to interact with websites without a visual display. 

If you don’t use a screen reader regularly, the way that you use it will be different to that of a habitual screen reader user, so be cautious in extrapolating your own experiences to those other users. But also bear in mind that not all regular screen reader users are experts or power users, just like not all users of web browsers are experts. 

If you’re a Mac user, VoiceOver is built-in to OSX and is a decent, basic screen reader. This guide from WebAIM [explains the basics of using VoiceOver to test pages](https://webaim.org/articles/voiceover/). 

If you’re a Windows user, NVDA is one of the more popular screen readers amongst blind users. This guide from WebAIM [explains the basics of using NVDA to test pages](https://webaim.org/articles/nvda/).
