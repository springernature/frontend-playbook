# Open source support


## Versioning

Our open source projects are versioned with [semver](semver.md). You should read through the [semver documentation](http://semver.org) if you're going to release new versions.


## Release process

To publish a new version of one of our open source projects:

* Switch to the `master` branch. Version commits are the only ones that shouldn't be committed to a feature branch.
* Increment either the major, minor, or patch version in the `package.json` file. If you're unsure which, check with the rest of the team or re-read the semver docs. Also verify if there are any mentions to the old version in the `README.md` or any other files, and update them too.
* Add an entry to the `HISTORY.md` file outlining the changes in the new version. Take your time, this log should be useful to developers who work on the project - it should help them make decisions about whether they can or should upgrade. If there are additional commits on the `master` branch since the last version, be sure to include a description of what they do in your history update - talk to the developers who committed them, if necessary.
* Commit your changes with a message formatted as `Version 1.2.3` - this helps people find version commits in the log.
* Tag your newly created commit with the version number. E.g. `git tag 1.2.3`. Do *not* prepend a `v` or `Version`, for example do not use neither `git tag v1.2.3` nor `git tag "Version 1.2.3"`.
* Push both the commit and the new tags to origin: `git push --follow-tags`. This will push both commits and only tags that are both annotated and reachable from the pushed commits. Do **not** use `git push --tags` as [you may inadvertely push bad tags](http://stackoverflow.com/questions/5195859/push-a-tag-to-a-remote-repository-using-git) (unannotated tags or annotated tags on unrelated branches) that may mess up your colleagues' repos.
* Depending of how the project is set up, the build system will automatically publish your new version based on the tag. Otherwise you may have to run `npm publish` to publish the package in [npm](https://www.npmjs.com/). If you don't have permission yet, request it from one of the existing collaborators, e.g. [https://www.npmjs.com/package/shunter/access](https://www.npmjs.com/package/shunter/access).


## CI tests

We aim for every project to run its unit tests automatically every time a change is commited to its repo.

At the moment we use [Travis CI](https://travis-ci.org/springernature/) for our projects but other options are available.

The `master` branch should be protected so other branches can't be merged unless the tests have passed on those branches.


## Node versions

On [node-based projects](https://nodejs.org) we aim to support every version that the Node foundation offers [Long-term support (LTS)](https://github.com/nodejs/LTS) for. That means that we won't offer support for odd versions like Node 5 and 7.

Additionally, on specific projects we may offer support for older versions of node (e.g. 0.12) when we consider it useful or necessary.

Dropping support for a node version from the test matrix must be only done as part of a major release, as we consider it a breaking change.


## Security

Whenever possible, we'll use automated tools and alerts in order to check for vulnerabilities in our projects or their dependencies.


## Suport for old versions

We aim to support old versions for 6 months after the next major version has been released. Support for old versions will be usually limited to security issues or important bugfixes.

