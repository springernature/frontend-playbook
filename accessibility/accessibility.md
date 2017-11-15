# Accessibility

* [What is accessibility](#what-is-accessibility)
* [Why we care about accessibility](#why-we-care-about-accessibility)
* [What standards we conform to](#what-standards-we-conform-to)
* [How we conform](#how-we-conform)
* [Find out more:](#find-out-more)


## What is accessibility

> The power of the Web is in its universality.
> Access by everyone regardless of disability is an essential aspect.
>
> _Tim Berners-Lee, inventor of the World Wide Web_

The Web is fundamentally designed to work for all people, whatever their hardware, software, language, culture, location, or physical or mental ability. When the Web meets this goal, it is accessible to people with a diverse range of hearing, movement, sight, and cognitive ability.

Thus the impact of disability is radically changed on the Web because the Web removes barriers to communication and interaction that many people face in the physical world. However, when websites, web technologies, or web tools are badly designed, they can create barriers that exclude people from using the Web.

It is essential that the Web be accessible in order to provide equal access and equal opportunity to people with diverse abilities. Indeed, the [UN Convention on the Rights of Persons with Disabilities](https://www.un.org/development/desa/disabilities/) recognises access to information and communications technologies, including the Web, as a basic human right.

Accessibility supports social inclusion for people with disabilities as well as others, such as older people, people in rural areas, and people in developing countries.


## Why we care about accessibility

From a technical standpoint, catering for all users complements our browser support policy (we aim to support all browsers), and our use of progressive enhancement.

From a moral standpoint, we have a duty to cater for all users regardless of disability. If we know that people can encounter difficulties accessing our content (which we do), and we know that we can do things to facilitate that access (which we do), then not making something accessible is knowingly contributing to the oppression of people with disabilities.

From a legal standpoint, we are required to comply with various pieces of equality legislation (e.g. the [2010 Equality Act](http://www.legislation.gov.uk/ukpga/2010/15/contents), and [Section 508](https://www.section508.gov/) of the US Rehabilitation Act 1973).

From a financial standpoint, a major benefit of Web accessibility is the potential for direct and indirect financial gains from increased website use.

Accessible sites can be used by more people - including people with disabilities, people using mobile devices, older people, people with low literacy, people who are not fluent in the language of the site, people with low bandwidth connections to the Internet, people with older technologies, and new and infrequent web users.

![Microsoft illustration of how designing for permanent disabilities helps many people facing temporary or situational disability](images/microsoft-accessibility.jpg)

(image &copy; Microsoft)


## What standards we conform to

In order to aid us in developing and maintaining an accessible website, we strive to comply with the [Web Content Accessibility Guidelines 1](https://www.w3.org/TR/WCAG10/) AA + the [WCAG Samurai Errata](http://www.wcagsamurai.org/erratas/introduction/). In doing so, we also achieve a high pass rate with [Web Content Accessibility Guidelines 2](https://www.w3.org/TR/WCAG20/) AA.


## How we conform

It's not enough to ensure that we build accessible sites - we need to ensure we maintain them as well - it's quite common for sites to degrade over time, as new features are added. To this end we use [pa11y](https://github.com/pa11y) - a tool that we developed in-house, to allow us to monitor the accessibility of our sites over time.

We have also created [a simple accessibility checklist](accessibility-checklist.md), to help people become familiar with the guidelines/standards, and to aid us when manually assessing pages.

Following guidelines is necessary, but including accessibility in the design process as soon as possible, is even more important. Only by working with disabled users and colleagues can we provide the sort of excellent results that - for instance - [gov.uk](https://www.gov.uk/) achieves.


## Find out more:

* [Accessibility in Media: Tip Sheet & Resources](https://ft-interactive.github.io/accessibility/index.html)

Some information in this page is taken from the Web Accessibility Initiative ([WAI](http://www.w3.org/WAI/)) document: _[Developing a Web Accessibility Business Case for Your Organization: Overview](https://www.w3.org/WAI/bcase/Overview)_. Copyright © [W3C](http://www.w3.org/)® ([MIT](http://www.csail.mit.edu/), [ERCIM](http://www.ercim.org/), [Keio](http://www.keio.ac.jp/)).
