# House style guide

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

We lint our CSS, JavaScript, and templates written with DustJS. This helps us to keep our different codebases consistent, avoid common logic and implementation errors, and lets us concentrate on solving problems instead of formatting.

* For DustJS templates, we use [Dustmite](https://www.npmjs.com/package/dustmite). You can find more details about how we write markup in our [markup guide](../markup/house-style.md).
* For CSS linting, we use [StyleLint](https://github.com/stylelint/stylelint) and [sass-lint](https://github.com/sasstools/sass-lint). You can find our configuration and examples in our [CSS style guide](../css/house-style.md).
* For JavaScript linting, we use [eslint](https://eslint.org/) with our own [eslint configuration](https://github.com/springernature/eslint-config-springernature). You can find our principles and best practices in the [JavaScript style guide](../javascript/house-style.md).

### Accessibility

We care a great deal about accessibility. Our target standards for all of our products are [WCAG 2.1](https://www.w3.org/TR/WCAG21/) level AA, in line with the current EU legislation, [EN 301 549](http://mandate376.standards.eu/standard). *All first and third party web products and components published by Springer Nature must conform to WCAG 2.1 AA.* 

Civil and federal legislation worldwide is converging on WCAG. Meeting WCAG 2.1 AA will also bring us into alignment with federal regulations like [US Section 508](https://www.section508.gov/) and [UK Accessibility Regulations 2018](https://www.legislation.gov.uk/uksi/2018/952/introduction/made), and with civil rights legislation like the [UK Equality Act 2010](http://www.legislation.gov.uk/ukpga/2010/15/contents) and the [Americans with Disabilities Act](https://www.ada.gov/2010_regs.htm). 

Read our [Accessibility guide](../accessibility/introduction.md) to understand how we meet these aims.

### Progressive enhancement and browser support

We support *all* browsers to different degrees of functionality. "Support" does *not* mean that everybody gets the same thing. Read our [browser support page](../practices/graded-browser-support.md) to understand our approach and where to aim your efforts.

Our approach to browser support means that you MUST practice progressive enhancement when building sites for Springer Nature, not graceful degradation. See the [progressive enhancement guide](../practices/progressive-enhancement.md) to understand what this means.

### Code review

We practice code review to safeguard the quality of what we produce. Code review aims to catch inadvertent mistakes, errors, and omissions (e.g. missing tests), and to act as a learning exercise for reviewers and reviewees.

Everyone is expected to review code submissions; your level of experience as a developer or with the codebase in question doesn't matter. When submitting code for review, be prepared to explain your thinking. When reviewing code, don't be afraid to ask the submitter to explain!

Read the [code review guide](../practices/code-review.md) for details on how we manage code reviews, and what to look for when reviewing.

### Written communications

Not all written communications need to follow house style - for e.g. we don't expect you to follow any rules in Slack, beyond what's expected of you as a professional. If you write for any of our open source repositories (including documentation), [Cruft.io](http://cruft.io/), or any of our [social media accounts](../writing/social-media.md), please familiarise yourself with the [Language guide](../writing/house-style.md). Always use [inclusive language](../writing/inclusive-language.md).

## Making changes to the house style

The playbook outlines our _current_ agreed house style. It's not written in stone, everybody has the opportunity to contribute and make changes. However, it's easy to [waste time and effort](https://en.wikipedia.org/wiki/Law_of_triviality) discussing code style. We use a process to make these discussions structured and productive.

If you would like to propose a change to house style, follow these steps:

1. Read the relevant page in the playbook (assuming it exists).
2. Understand that you SHOULD NOT deviate from this style unless there are valid reasons in particular circumstances when the particular behaviour is acceptable or even useful.
3. If you believe that your situation or case meets the criteria in point 2, detail to the rest of the team the benefits of making an exception or a change.
4. If the team agrees that your exception (or change) is acceptable and useful, submit a PR to the playbook, detailing the exception (or change) to the world.
