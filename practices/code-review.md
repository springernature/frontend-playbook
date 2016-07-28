# Code Reviews

Code Review, or Peer Code Review, is the act of having your code checked by other front-end developers for mistakes, errors, and omissions (e.g. missing tests). It has been repeatedly shown to accelerate and streamline the process of software development.

We manage code review via **pull requests**, which we communicate in the `#front-end-pr` Slack channel, and manage in GitHub. All discussion happens in GitHub comments. We leave it to the requester to merge their own changes -- we never merge someone else's work!

## Why?

- PR reviews are cross-team
    - allows greater visibility on other teams work
    - allows for standardisation of methodology across teams
    - allows more junior members of staff to learn best practices quicker
    - allows EVERYONE to learn from their colleagues
    - facilitates people moving to other teams as they are more familiar with the codebase
- Ensure that frontend developers within each team are coding to the same guidelines
- Fosters discussion and collaboration
- Having someone who has not worked on the ticket look at it is a good way to spot logic errors and bugs
- Prepares people for work on open source software projects

## How

Here's the general protocol that we use:

1. Create a local feature branch based off master.
* When feature is complete and tests pass, stage the changes and commit them.
* Write a [good commit message](practices/commit-messages.md).
* Submit a [pull request](https://help.github.com/articles/using-pull-requests/).
* Ask for a code review in Slack.
* A team member other than the author reviews the pull request, and they make comments and ask questions directly on lines of code in the GitHub web interface.
* When satisfied, the reviewer will comment on the pull request with a +1 or some other simple message indicating that the code is ready to merge.
* Rebase interactively. Squash commits like "Fix whitespace", or micro-commits that serve no purpose without the following commits into one or a small number of valuable commit(s). Edit commit messages to reveal intent.
* View a list of new commits. View changed files. Merge branch into master.
* Delete your remote feature branch.
* Delete your local feature branch.