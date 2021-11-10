# Code reviews

* [Why](#why)
* [What to look out for](#what-to-look-out-for)

Code Review, or Peer Code Review, is the act of having your code checked by others for mistakes, errors, and omissions (e.g. missing tests). Like pair-programming (which we also support), it accelerates and streamlines software development.

While we can support "traditional" Code Reviews, [we routinely review via **pull requests**](../git/git.md#pull-requests). These are communicated in the `#frontend-pr` Slack channel, and managed via GitHub. Discussion should happen in the GitHub comments, not Slack.

Requesters merge their own changes when they're ready. Keep your fingers off that tempting green merge button. 


## Why do them?

**PR reviews are cross-team, thereby helping to foster discussion and feedback**

1. Knowledge sharing and transfer within and between teams:
	* Allows everyone to learn from their colleagues.
	* Allows greater visibility and familiarity of other team's work.
	* Helps prevent knowledge silos or domain-specific codebases.
	* Allows FEDs to share expertise.
1. Standards compliance across teams:
	* Aids the ability for developers to easily move between teams.
	* Ensures changes to codebase conforms to the same standards and guidelines.
	* Helps identify areas where code re-use are beneficial ("should that be a component?").
	* Helps identify areas of compliance, which are missed during development.
	* Fosters caution and code quality over temporary hacks.
1. Prepares people for work on [open source software projects](https://github.com/springernature/open-source-directory).
1. Generally aids onboarding and training.


## What to look out for

* **Accessibility**

  * [Accessibility](../accessibility/accessibility-checklist.md) problems. Suggest testing with [pa11y](https://github.com/pa11y) and/or other tools.
    * [pa11y dashboard](http://pa11y.springernature.com/) _(link only works if inside the Springer Nature VPN)_

* **Complexity**

  * [Overly complex code](https://www.codesimplicity.com/post/what-is-overengineering/): code that solves problems we don't have, or makes things more complex instead of less.
  * Code that introduces [out-of-date](https://docs.npmjs.com/cli/outdated) or unnecessary dependencies into the project.
  * Changes which may have wider ramifications than the author anticipated. Double check they are aware which can of worms they have just opened :)

* **Performance**

  * [Premature](http://wiki.c2.com/?PrematureOptimization) and/or micro optimisations.
  * Non-performant code. Suggest testing with [Lighthouse](https://developers.google.com/web/tools/lighthouse/), [SpeedCurve](https://speedcurve.com), [WebPageTest](https://www.webpagetest.org/) and/or other tools.

* **Scope**

  * [PRs which are non-atomic](https://medium.com/@fagnerbrack/one-pull-request-one-concern-e84a27dfe9f1) and should be split into separate PRs, e.g. a new UI feature combined with an unrelated configuration change.
  * Code which could be split up into reusable modules.

* **Security**

  * Code that introduces potential vulnerabilities. Suggest testing with [Snyk](https://snyk.io) and/or other tools.

* **Syntax**
  * Syntactic inconsistencies the [linter](https://github.com/springernature/frontend-playbook/blob/master/practices/house-style.md#linting) did not catch.
