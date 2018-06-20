# Code reviews

* [Why](#why)
* [How](#how)
* [What to look out for](#what-to-look-out-for)

Code Review, or Peer Code Review, is the act of having your code checked by others for mistakes, errors, and omissions (e.g. missing tests). Like pair-programming (which we also support), it accelerates and streamlines software development.

While we can support "traditional" Code Reviews, we routinely review via **pull requests**. These are communicated in the `#frontend-pr` Slack channel, and managed via GitHub. Discussion should happen in the GitHub comments, not Slack.

We leave it to the requester to merge their own changes when they are ready, because sometimes the requester might not want their work merged immediately.


## Why

1. PR reviews are cross-team;
    * allows everyone to learn from their colleagues.
    * allows greater visibility of other teams work.
    * FED works encompasses many areas of expertise, and no-one is expert in more than 2 or 3 areas.
    * facilitates people moving to other teams as they are more familiar with the codebase.
    * helps prevent knowledge silos.
    * helps identify areas where code re-use may be of benefit ("should that be a component?").
    * if the code requires so much domain-specifc knowledge it cannot be understood by other teams, maybe that code needs refactoring?
    * generally aids onboarding and training.
1. Ensure that any changes to front-end code conforms to the same standards and guidelines.
1. Fosters discussion and collaboration.
1. Fosters caution and code quality over temporary hacks.
1. Prepares people for work on [open source software projects](https://github.com/springernature/open-source-directory).


## How

Here's the general process that we use:

1. Create a local branch based off master.
1. Branches should adhere to the following best practices to ensure they align with [Continous Delivery](https://martinfowler.com/bliki/ContinuousDelivery.html) & [Continuous Integration](https://martinfowler.com/articles/continuousIntegration.html) as much as is reasonable (given the constraints of team structure and the discipline);
	* Branches should be as short lived as possible.
	* Branches should be _atomic_ i.e. one unit of work that cannot be sensibly subdivided.
		* Therefore they should contain their own tests.
		* Therefore they should be releasable independently.
	* Branches should be as limited in scope as possible. Large PR's are hard to review and can be painful to merge. Also, once merged & a bug is traced back to that commit, they are much harder to debug.
1. When you are getting close to being ready for PR, `git rebase master` or merge -- especially if other devs are working on the same code. Avoid merge pain by;
	* _talking to your team_ to divide work across files sensibly & co-ordinate merges if required.
	* pull origin master & rebase or merge often.
	* make sure branches are short-lived! (Did we mention that branches should be short-lived?)
1. When the unit of work is complete and tests pass, stage the changes and commit them.
1. Write a [good commit message](../git/git.md#commit-messages).
1. Submit a [pull request](https://help.github.com/articles/using-pull-requests/).
1. Ask for a code review in Slack.
1. A colleague (or multiple colleagues) other than the author reviews the pull request, and they make comments and ask questions directly on lines of code in the GitHub web interface.
1. When satisfied, the reviewer(s) will approve the pull request indicating that the code is ready to merge.
1. Give your code one last visual check in github.
1. Double-check the commit message -- and any commit message detail -- then **"Squash & Merge" commits via github**. We do not want lots of "work in progress" commits cluttering the commit history on master. _One unit of work, one commit._
1. Delete your remote branch.
1. (Optional) Delete your local branch.

### What about GitHub's pull request reviews?

[GitHub's pull request reviews feature](https://help.github.com/articles/about-pull-request-reviews/) programatically blocks merging of the code until it has been reviewed, thereby preventing the developer who opened the PR from merging themselves. This feature may or may not be enabled on a repository, at the discretion of the individual team.

## What to look out for

* Are there syntactic inconsistencies the linter did not catch?
* Overly complex code.
* PRs which are non-atomic and should be split into separate PRs, e.g. a new UI feature combined with an unrelated configuration change.
* Code which could be split up into reusable modules.
* Non-performant code. Suggest testing with [WebPageTest](https://www.webpagetest.org/) and/or other tools.
* Inaccessible code. Suggest testing with [pa11y](https://github.com/pa11y) and/or other tools.
    * [internal-only pa11y dashboard](http://pa11y.springernature.com/)
* Do you see something which may have wider ramifications than the author anticipated? Double check they are aware which can of worms they have just opened :)
