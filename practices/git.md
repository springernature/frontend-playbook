# Repositories

We use a standard naming format for our Git repositories. Repository names are train-case (all lowercase, words separated by a hyphen), and begin with "frontend" followed by your project name. 

We _don't_ do this:

```
front-end-project-name
front-end-projectname
project-name-front-end
project-name-frontend
```

We do this:

```
frontend-project-name
```


# Commit Messages

Your commit messages are your personal legacy.

They are the record of what you've done to a codebase and more importantly, *why*.

* Make the first line [50 characters or less](http://stopwritingramblingcommitmessages.com/), followed by a blank line.
* Add more explanatory text if necessary, as detailed as you need. But please make lines wrap at 72 characters.
* If the work was done in relation to a ticket, include the ticket number in the commit message. **DON'T** only use the ticket number — this just makes life hard for your colleagues to understand what the change was for. The git log should be all they need to read.
* Unhelpful messages like "Update" or "Bugfix" are... _unhelpful_. Please explain a little more.

One useful tip for writing great commit messages: imagine your commit message has to make sense prefaced with _"If applied, this commit will..."_.

A few blog posts on writing better commit messages:

* [5 Useful Tips for a Better Commit Message](https://robots.thoughtbot.com/5-useful-tips-for-a-better-commit-message)
* [A Note About Commit Messages](http://tbaggery.com/2008/04/19/a-note-about-git-commit-messages.html)
* [Git Commit](http://chris.beams.io/posts/git-commit/)
* [Writing Good Commit Messages](https://github.com/erlang/otp/wiki/Writing-good-commit-messages)
* [Better Commit Messages with a `.gitmessage` Template](https://robots.thoughtbot.com/better-commit-messages-with-a-gitmessage-template)


# Contributing

* Always submit pull requests for any changes. [Version commits](#Versioning) are the only commits that shouldn't be in a pull-request.
* Please delete the branch from the remote after the pull request has been merged.


# Versioning

Our open source projects are versioned with [semver](semver.md). You should read through the [semver documentation](http://semver.org) if you're going to release new versions.

To publish a new version of one of our projects:

* Switch to the `master` branch. Version commits are the only ones that shouldn't be committed to a feature branch.
* Increment either the major, minor, or patch version in the `package.json` file. If you're unsure which, check with the rest of the team or re-read the semver docs.
* Add an entry to the `HISTORY.md` file outlining the changes in the new version. Take your time, this log should be useful to developers who work on the project. If there are additional commits on the `master` branch since the last version, be sure to include a description of what they do in your history update – talk to the developers who committed them.
* Commit your changes with a message formatted as `Version 1.2.3` – this helps people find version commits in the log.
* Tag your newly created commit with the version number only, e.g. `git tag 1.2.3`. Do not use neither `git tag v1.2.3` nor `git tag "Version 1.2.3"`.
* Push both the commit and the new tags to origin: `git push --follow-tags`. This will push both commits and only tags that are both annotated and reachable from the pushed commits. Do **not** use `git push --tags` as [you may inadvertely push bad tags](http://stackoverflow.com/questions/5195859/push-a-tag-to-a-remote-repository-using-git) (unannotated tags or annotated tags on unrelated branches) that may mess up your colleagues' repos.
* If the project is open source, run 'npm publish' to publish the package in [npm](https://www.npmjs.com/). If you don't have permission yet, request it from one of the existing collaborators, e.g. [https://www.npmjs.com/package/shunter/access](https://www.npmjs.com/package/shunter/access).
