# Git

* [Repositories](#repositories)
* [Commit Messages](#commit-messages)
* [Versioning](#versioning)

## Repositories

We use a standard naming format for our Git repositories. Repository names are _lowercase-hyphenated_ (all lowercase, words separated by a hyphen), and begin with "frontend" followed by your project name.

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

## Commit Messages

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

## Versioning

Our open source projects are versioned with [SemVer](semver.md). Check our [Open Source support](../open-source-support.md) guide for details on how to version and release an update to an open source project.
