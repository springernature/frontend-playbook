# Code reviews

* [Why](#why)
* [How](#how)
* [What to look out for](#what-to-look-out-for)


Code Review, or Peer Code Review, is the act of having your code checked by others for mistakes, errors, and omissions (e.g. missing tests). Like pair-programming (which we also support), it accelerates and streamlines software development.

We manage code review via **pull requests**, which we communicate in the `#frontend-pr` Slack channel, and manage in GitHub. All discussion happens in GitHub comments. We leave it to the requester to merge their own changes when they are ready, because sometimes the requester might not want their work merged immediately.

## Why

* PR reviews are cross-team.
    * allows greater visibility of other teams work.
    * allows for standardisation of methodology across teams.
    * allows more junior members of staff to learn best practices quicker.
    * allows EVERYONE to learn from their colleagues.
    * facilitates people moving to other teams as they are more familiar with the codebase.
* Ensure that any changes to front-end code conforms to the same standards and guidelines.
* Fosters discussion and collaboration.
* Having someone who has not worked on the ticket look at it is a good way to spot architectural inconsistencies (required or not). This is especially noticeable when review is performed by people from different teams.
* Prepares people for work on open source software projects.

## How

Here's the general protocol that we use:

1. Create a local branch based off master.
1. Branches should adhere to the following best practices to ensure they align with [Continous Delivery](https://martinfowler.com/bliki/ContinuousDelivery.html) & [Continuous Integration](https://martinfowler.com/articles/continuousIntegration.html) as much as possible;
	* atomic i.e. one unit of work that cannot be sensibly broken up into smaller parts. (Therefore they should contain their own tests.)
	* as limited in scope as possible. Massive PR's are hard to review, more painful to merge, and once merged & a bug is traced back to that commit, harder to debug.
	* as short lived as possible.
	* releasable independently. 
1. When you are getting close to being ready for PR, `git rebase master` -- especially if other devs are working on the same code.  Avoid rebase hell by;
	* _talking to your team_ to divide work across files sensibly & co-ordinate merges if required.
	* pull origin master & rebase often.
	* make sure branches are short-lived! (Did we mention that branches should be short-lived?)
1. When the unit of work is complete and tests pass, stage the changes and commit them.
1. Write a [good commit message](../git/git.md#commit-messages).
1. Submit a [pull request](https://help.github.com/articles/using-pull-requests/).
1. Ask for a code review in Slack.
1. A colleague (or multiple colleagues) other than the author reviews the pull request, and they make comments and ask questions directly on lines of code in the GitHub web interface.
1. When satisfied, the reviewer(s) will comment on the pull request with a +1 or some other simple message indicating that the code is ready to merge.
1. Give your code one last visual check in github.
1. Double-check the commit message, and any commit message detail, then "Squash & Merge" commits via github. We do not want lots of "work in progress" commits cluttering master. One unit of work, one commit, makes debugging much easier.
1. Delete your remote branch.
1. Delete your local branch.

## What to look out for

* Are there syntactic inconsistencies that the linter did not catch?
* Overly complex code.
* PRs which are non-atomic and should be split into separate PRs, e.g. a new UI feature combined with an unrelated configuration change.
* Code which could be split up into reusable modules.
* Non-performant code. Suggest testing with [WebPageTest](https://www.webpagetest.org/) and/or other tools.
* Inaccessible code. Suggest testing with [pa11y](https://github.com/pa11y) and/or other tools.
    * [private Springer Nature instance of pa11y](http://pa11y-dashboard.dev.cf.springer-sbm.com/)
* Do you see something which may have wider ramifications than the author anticipated? Double check they are aware which can of worms they have just opened :)
