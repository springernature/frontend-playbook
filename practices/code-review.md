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
* Ensure that Front-End Developers within each team are coding to the same guidelines.
* Fosters discussion and collaboration.
* Having someone who has not worked on the ticket look at it is a good way to spot logic errors and bugs.
* Prepares people for work on open source software projects.

## How

Here's the general protocol that we use:

1. Create a local short-lived feature branch based off master.
* When feature is complete and tests pass, stage the changes and commit them.
* Write a [good commit message](git/git.md#commit-messages).
* Submit a [pull request](https://help.github.com/articles/using-pull-requests/).
* Ask for a code review in Slack.
* A colleague (or multiple colleagues) other than the author reviews the pull request, and they make comments and ask questions directly on lines of code in the GitHub web interface.
* When satisfied, the reviewer(s) will comment on the pull request with a +1 or some other simple message indicating that the code is ready to merge.
* Rebase interactively. Squash commits like "Fix whitespace", or micro-commits that serve no purpose without the following commits into one or a small number of valuable commit(s). Edit commit messages to reveal intent.
* View a list of new commits. View changed files. Merge branch into master.
* Delete your remote feature branch.
* Delete your local feature branch.

## What to look out for

* Are there syntactic inconsistencies within the code? Suggest using a linter to scan for such problems automatically.
* Overly complex code.
* Code which could be split up into reusable modules.
* Non-performant code. Suggest testing with [WebPageTest](https://www.webpagetest.org/) and/or other tools.
* Inaccessible code. Suggest testing with [pa11y](https://github.com/pa11y) and/or other tools.
    * [private Springer Nature instance of pa11y](http://pa11y-dashboard.dev.cf.springer-sbm.com/)
* Do you see something which may have wider ramifications than the author anticipated? Double check they are aware which can of worms they have just opened :)
