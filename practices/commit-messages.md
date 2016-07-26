# Commit Messages

Your commit messages are your personal legacy - they are the record of what you have done to a codebase and more importantly, *why*. We find commit messages are most useful when we follow a small set of rules:

* The first line should always be [50 characters or less](http://stopwritingramblingcommitmessages.com/) and that it should be followed by a blank line.
* Following the short 50 character summary, add more detailed explanatory text if necessary, and make it as long/detailed as you need, there's no limits here, but please make the lines wrap at 72 characters.
* If this work was done in relation to a Jira/Trello/whatever ticket, reference the ticket number in the commit message, but **DO NOT** use the ticket number as the entire commit message - this just makes it annoying for your colleagues to see what this change was for. The git log should be all they need to read to understand this change.
* Super short commit messages like "Update", or "Bugfix" are unacceptable - please explain a little more about the change.

If you need a bit more inspiration for writing better commit messages, please check out these great blog posts on the subject:

* [5 Useful Tips for a Better Commit Message](https://robots.thoughtbot.com/5-useful-tips-for-a-better-commit-message)
* [A Note About Commit Messages](http://tbaggery.com/2008/04/19/a-note-about-git-commit-messages.html)
* [Git Commit](http://chris.beams.io/posts/git-commit/)
* [Writing Good Commit Messages](https://github.com/erlang/otp/wiki/Writing-good-commit-messages)
* [Better Commit Messages with a `.gitmessage` Template](https://robots.thoughtbot.com/better-commit-messages-with-a-gitmessage-template)