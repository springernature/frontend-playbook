House style guide
=================

This document outlines the reasons for our having a house style, and generally-applicable principles. It's a living styleguide – it will grow as our practices do.

- [Rationale](#rationale)
- [General Principles](#general-principles)
  - [Linting](#linting)
  - [Accessibility](#accessibility)
  - [Progressive enhancement and browser support](#progressive-enhancement-and-browser-support)
  - [Code review](#code-review)
  - [Written communications](#written-communications)
- [Making changes to the house style](#making-changes-to-the-house-style)


## Rationale

The benefits of choosing one house style outweigh the benefits of allowing people free rein with code style. Personal preference is outweighed by the greater good. This isn't to say that we shouldn't constantly be looking to improve our ways of working. We aim to reduce friction for ourselves as we move between teams, and we do this by maintaining a general house style, linting, and agreeing on common practices.

Read this excellent [article by Nicholas C. Zakas](https://www.smashingmagazine.com/2012/10/why-coding-style-matters/) to understand why having a house style is important.


## General principles

Read the [markup guide](../markup/house-style.md), the [JavaScript guide](../javascript/house-style.md) and the [CSS guide](../css/house-style.md) to understand our house style in these technologies. You should also familiarise yourself with our [Git](../git/git.md) strategies. The team you're deployed to may also have its own strategies in addition to these.

### Linting

We lint our CSS, JavaScript, and templates written with DustJS. This helps us to keep our codebases consistent, avoid common logic and implementation errors, and lets us concentrate on solving problems instead of formatting.

* For CSS, use [StyleLint](https://github.com/stylelint/stylelint)
* For JavaScript, use [XO](https://github.com/sindresorhus/xo)
* For DustJS, use [Dustmite](https://www.npmjs.com/package/dustmite)

See the [CSS](../css/house-style.md), [JavaScript](../javascript/house-style.md), and [markup](../markup/house-style.md) guides for further details.

### Accessibility 

We care a great deal about accessibility. We aim to comply with the [Web Content Accessibility Guidelines 1](https://www.w3.org/TR/WCAG10/) AA + the [WCAG Samurai Errata](http://www.wcagsamurai.org/erratas/introduction/). In doing so, we also achieve a high pass rate with [Web Content Accessibility Guidelines 2](https://www.w3.org/TR/WCAG20/) AA. All of our websites MUST comply with [US Section 508](https://www.section508.gov/) and [UK Equality Act 2010](http://www.legislation.gov.uk/ukpga/2010/15/contents). As of January 18th 2018, WCAG 2.0 AA will be incorporated into Section 508. 

Read our [Accessibility guide](../accessibility/house-style.md) to understand how we meet these aims.

### Progressive enhancement and browser support

We support *all* browsers to different degrees of functionality. "Support" does *not* mean that everybody gets the same thing. Read our [graded browser support page](../practices/graded-browser-support.md) to understand our approach and where to aim your efforts.

Using graded browser support means that you MUST practice progressive enhancement when building sites for Springer Nature, not graceful degradation. See the [progressive enhancement guide](../practices/progressive-enhancement.md) to understand what this means.

### Code review

We practice code review to safeguard the quality of what we produce. Code review aims to catch inadvertent mistakes, errors, and omissions (e.g. missing tests), and to act as a learning exercise for reviewers and reviewees.

Everyone is expected to review code submissions; your level of experience as a developer or with the codebase in question doesn't matter. When submitting code for review, be prepared to explain your thinking. When reviewing code, don't be afraid to ask the submitter to explain!

Read the [code review guide](../practices/code-review.md) for details on how we manage code reviews, and what to look for when reviewing.

### Written communications

Not all written communications need to follow house style - for e.g. we don't expect you to follow any rules in Slack, beyond what's expected of you as a professional. If you write for any of our open source repositories (including documentation), [Cruft.io](http://cruft.io/), or any of our [social media accounts](../writing/social-media.md), please familiarise yourself with the [Language guide](../writing/language.md).


## Making changes to the house style

The playbook outlines our _current_ agreed house style. It's not written in stone, everybody has the opportunity to contribute and make changes. However, it's easy to [waste time and effort](https://en.wikipedia.org/wiki/Law_of_triviality) discussing code style. We use a process to make these discussions structured and productive.

If you would like to propose a change to house style, follow these steps:

1. Read the relevant page in the playbook (assuming it exists).
2. Understand that you SHOULD NOT deviate from this style unless there are valid reasons in particular circumstances when the particular behavior is acceptable or even useful.
3. If you believe that your situation or case meets the criteria in point 2, detail to the rest of the team the benefits of making an exception or a change.
4. If the team agrees that your exeption (or change) is acceptable and useful, submit a PR to the playbook, detailing the exception (or change) to the world.
