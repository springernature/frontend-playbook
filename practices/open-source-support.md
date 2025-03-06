# Open source support

- [Versioning](#versioning)
- [Release process](#release-process)
- [CI tests](#ci-tests)
- [Node versions](#node-versions)
- [Security](#security)
- [Support for old versions](#support-for-old-versions)


## Versioning

Our open source projects are versioned with [SemVer](../git/semver.md). You should read through the [SemVer documentation](http://semver.org) if you're going to release new versions.


## Release process

To publish a *new* version of one of our open source projects:

* Switch to the default branch. Version commits are the only ones that shouldn't be committed to a feature branch.
* Consider what type of release this is: `major`, `minor` or `patch` according to SemVer. If you're unsure which, check with the rest of the team or re-read the [SemVer docs](https://semver.org/). Also verify if there are any mentions to the old version in the `README.md` or any other files, and update them too.
* Add an entry to the `HISTORY.md` file outlining the changes in the new version. Take your time, this log should be useful to developers who use this project - it should help them make decisions about whether they can or should upgrade. If there are additional commits on the default branch since the last version, be sure to include a description of what they do in your history update - talk to the developers who committed them, if necessary.
* Run `npm version` depending on the SemVer type of release - e.g. `npm version minor` for a minor release. This will:
  * increment the version in your `package.json`, based on the type of release.
  * commit this version bump.
  * create a tag for the current release in your local repository.
* You can also use the above command to conveniently publish a release candidate, e.g. `npm version 4.0.0-rc1`. Once you are finished with the release candidates and ready for a major release, use `npm version major`.
* It's possible to do those steps manually, but using this convenience method of `npm` reduces human error and increases consistency.
* Before publishing to NPM for real, run `npm publish --dry-run` ([docs](https://docs.npmjs.com/cli/v9/commands/npm-publish#dry-run)) to see what will happen.
* Push both the commit and the new tags to origin: `git push && git push --tags`.
* Depending on how the project is set up, the build system may automatically publish your new version based on the tag. Otherwise you may have to run `npm publish` to publish the package in [npm](https://www.npmjs.com/). If you don't have permission yet, request it from one of the existing collaborators.


## CI tests

We aim for every project to run its unit tests automatically every time a change is committed to its repo.

At the moment we recommend [GitHub Actions](https://docs.github.com/en/actions/use-cases-and-examples/building-and-testing/building-and-testing-nodejs) for our projects but other options are available.

The default branch should be protected so other branches can't be merged unless the tests have passed on those branches.


## Node versions

On [node-based projects](https://nodejs.org) we aim to support every version that the Node foundation offers [Long-term support (LTS)](https://github.com/nodejs/Release) for. That means that we won't offer support for odd versions like Node 19 and 21.

Dropping support for a node version from the test matrix must be only done as part of a major release, as we consider it a breaking change.


## Security

Whenever possible, we'll use automated tools and alerts in order to check for vulnerabilities in our projects or their dependencies.


## Support for old versions

We aim to support old versions for 6 months after the next major version has been released. Support for old versions will be usually limited to security issues or important bugfixes.

