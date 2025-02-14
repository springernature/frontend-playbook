# Managing Node.js-based projects and dependencies

* [Installing dependencies](#installing-dependencies)
  * [`npm install`](#npm-install)
  * [`npm ci`](#npm-ci)
  * [How to specify the version of node to use](#how-to-specify-the-version-of-node-to-use)
    * [`nvm` usage](#nvm-usage)
    * [Automatically running `nvm use`](#automatically-running-nvm-use)
  * [Should I check in `package-lock.json` to version control?](#should-i-check-in-package-lockjson-to-version-control)
  * [Managing changes to the `package-lock.json` file](#managing-changes-to-the-package-lockjson-file)
* [Specifying versions of dependencies](#specifying-versions-of-dependencies)
  * [Run-time dependencies](#run-time-dependencies)
    * [Examples](#examples)
  * [Development dependencies](#development-dependencies)
    * [Examples](#examples-1)
  * [Classifying "built" run-time dependencies](#classifying-built-run-time-dependencies)
* [Configuration](#configuration)
* [Publishing projects on NPM](#publishing-projects-on-npm)
  * [Naming projects](#naming-projects)
* [Open source dependencies](#open-source-dependencies)
* [Handling dependencies from third parties](#handling-dependencies-from-third-parties)

This guide describes how we use node and manage package dependencies in [Springer Nature Node.js-based projects](https://github.com/springernature?utf8=%E2%9C%93&q=&type=public&language=javascript).


## Installing dependencies

There are two methods for installing all dependencies for a node project: `npm install` and `npm ci`.

### `npm install`

`npm install` is the most common method; but it doesn't guarantee the project will build consistently. This is because `npm` can install varying versions of dependencies according to [semantic versioning](https://docs.npmjs.com/files/package.json#dependencies), and _possibly_ the version of node used when installing.

If a `package-lock.json` file is not already present, `npm install` will create it. `package-lock.json` describes the complete dependency tree and exact versions of all dependencies required.

But - **`npm install` does not use `package-lock.json` as the source of authority for what to install.** This is why it results in inconsistent builds.

Another potential problem - when developing an application, it's common to try out various packages until you find one you like, adding them to the `package.json` as you go. But, removing a package from `package.json` does not remove the package from your `node_modules` folder, and neither does a subsequent `npm install`. So it's possible for your code to reference packages still on your machine that are no longer in the `package.json`, and that code will break for anyone doing a fresh install (including CI).

All that said, `npm install` is the method we recommend for installing dependencies when authoring node _libraries_ (for complex reasons we won't discuss here).

### `npm ci`

`npm ci` is much simpler to understand. It installs the complete dependency graph exactly as specified in the `package-lock.json` file, and so guarantees consistent builds. This helps reduce "but it works on my machine" issues and is suitable for CI/CD environments (as the name implies).

[`npm ci` is also much quicker than `npm install`](https://docs.npmjs.com/cli/ci.html#description) if the `./node_modules` directory is not present (such as in a CI environment).

`npm ci` is the method we recommend for installing dependencies when authoring node _applications_. This is probably what you are doing, and so probably what you should use.

### How to specify the version of node to use

Specifying the expected node version makes compatibility requirements explicit to developers working on your application, and also deployment environments bulding your project.

There are two main ways of doing this, and it's important to use at least one:

1. The [`engines`](https://docs.npmjs.com/files/package.json#engines) field in `package.json`:
     * `engines` is important if you're authoring _libraries_. Let's assume we're using a different version of node to that specified in `engines` field for package `foo`.
     When you run `npm install` to install `foo`'s dependencies, `npm` will warn about the problem.
     When `npm install`ing a package _which depends on_ `foo`, `npm` will warn.

2. Using an `.nvmrc` file:
     * An `.nvmrc` file is a configuration file for `nvm` ([Node Version Manager](https://github.com/nvm-sh/nvm)).
     * Your _application_ should include an [`.nvmrc` file](https://github.com/nvm-sh/nvm?tab=readme-ov-file#nvmrc) in the root directory of the project to specify which version(s) of node are compatible.
     * It makes life much easier when working on multiple node projects locally that require different versions of node.
    
#### `nvm` usage

When you first check out a project, you should run `nvm use` before `npm ci` to ensure you're using the version of node the project requires.

#### Automatically running `nvm use`

But it's easy to forget to run `nvm use`!

To avoid forgetting, there are [shell extensions which run `nvm` automatically](https://github.com/nvm-sh/nvm#calling-nvm-use-automatically-in-a-directory-with-a-nvmrc-file) when `cd`-ing into a directory with an `.nvmrc` file in its hierarchy. Well worth installing!

### Should I check in `package-lock.json` to version control?

Yes. There are two main reasons:

1. Predictable builds, as discussed above.
1. Dependency analysis tools (such as `npm audit` and Dependabot) can spot insecure dependencies anywhere in the dependency tree by analysing the `package-lock.json` file. These tools can force updates of insecure dependencies in the tree, without waiting for third-party package maintainers to release fixes. This wouldn't be possible without a `package-lock.json` and is a huge benefit.

The downside is it requires all developers to use `nvm` and `npm ci` to install dependencies, otherwise there will be constant conflicts in the `package-lock.json` file.

### Managing changes to the `package-lock.json` file

Firstly, bear in mind machine-generated files should not be hand-edited, including `package-lock.json`.

Secondly, if you're seeing unexpected merge conflicts in `package-lock.json` it can be a symptom of someone using `npm install` instead of `npm ci`. Speak to the developer and see if they are having trouble.

When you update your dependencies and need to commit changes to `package-lock.json`, we strongly recommend commiting the minimal amount of changes to keep the application running - i.e. that you are especially careful to practice "[Atomic Commits](https://codesignal.com/learn/courses/git-basics/lessons/commits-in-detail-making-them-atomic-crafting-messages-and-using-amendments)".

## Specifying versions of dependencies

As a general rule, we tend to follow a conservative approach when specifying versions for the dependencies of our packages. We recommend PATCH version ranges for [run-time dependencies](#run-time-dependencies) and MINOR + PATCH version ranges for [dev dependencies](#development-dependencies). This helps us ensure consistency between different environments, (as we can't know for sure in what environment the app is going to be running), and helps prevent breakage caused by major or minor updates in dependencies.

We find that the this approach strikes a good balance between the potential breakage caused by less restrictive versions and the maintenance needed when restricting the dependencies to a specific version through the use of `npm shrinkwrap` or similar tools.

We use some [dependency management tools](#dependency-management-tools) to help us keep our apps up to date when new versions of their dependencies are released.

### Run-time dependencies

[Run-time dependencies](https://docs.npmjs.com/files/package.json#dependencies) are modules that are required for your application to run, independently of the environment or mode (e.g. development vs production) used.

These are defined in the `dependencies` section of the `package.json` file.

Version numbers for run-time dependencies are defined using a tilde `~` plus a full version number in the `MAJOR.MINOR.PATCH` form. For a package version specified as `~2.3.4` this means that all releases from `2.3.4` (inclusive) up to, but not including `2.4.0` are acceptable.

Specifying the versions in this way ensures that:

* We can easily get bugfixes made to the dependencies when these have been released as a PATCH.
* We don't expose the users of our modules to an unnecessary risk if one of our dependencies releases a MINOR update that breaks our app.
* Dependencies in early lifecycle projects (Version `0.MINOR.PATCH`) are traditionally considered of beta quality, or undergoing heavy development, and any minor could potentially contain breaking changes. Limiting the scope to PATCH updates heavily reduces the chance of our app breaking.
* The behaviour when installing the dependencies is basically as predictable as possible ([Principle of least astonishment](https://en.wikipedia.org/wiki/Principle_of_least_astonishment)) without the use of npm-shrinkwrap or similar tools.

Don't use wildcards (i.e. `*`, `x`) in the package numbers, or keywords like `latest`. Not only they make the version numbers harder to read but they also make it harder to predict what exact versions will be installed.

If you use `npm install --save` a lot, you may want to change npm's config so it uses tilde by default when saving dependencies:

```sh
npm config set save-prefix '~'
```

#### Examples

We do this:
```json
{
  "dependencies": {
    "boomcatch": "~1.2.0",
    "dustmite": "~1.0.0",
    "hasbin": "~0.8.0",
    "shunter": "~4.2.1",
    "thundermole": "~1.0.3",
    "truffler": "~1.1.0"
  }
}
```

We _don't_ do this:
```json
{
  "dependencies": {
    "boomcatch": "latest",
    "dustmite": "*",
    "hasbin": "~1.1",
    "shunter": "~4",
    "thundermole": "^1.0.3",
    "truffler": "~1.x"
  }
}
```

[Optional dependencies](https://docs.npmjs.com/files/package.json#optionaldependencies), if present, should also use the same format as run-time dependencies.

### Development dependencies

[Development dependencies](https://docs.npmjs.com/files/package.json#devdependencies) are required during the development, testing, or build process of the app. For example, you may include a test runner, a minifier, a bundler, etc.

These are defined in the `devDependencies` section of the `package.json` file and are not used in production environments.

Version numbers for development dependencies are defined using a caret `^` plus a full version number in the `MAJOR.MINOR.PATCH` form. For a package version specified as `^2.3.4` this means that all releases from `2.3.4` (inclusive) up to, but not including `3.0.0` are acceptable.

#### Examples

We do this:

```json
{
  "devDependencies": {
    "jscs": "^2.0.0",
    "mocha": "^3.1.0",
    "xo": "^1.1.1"
  }
}
```

We _don't_ do this:
```json
{
  "dependencies": {
    "jscs": "latest",
    "mocha": "*",
    "xo": "~1.1.1",
  }
}
```

### Classifying "built" run-time dependencies

While the classification of run-time and development dependencies is usually fairly clear-cut, there can be grey areas.  For example, dependencies that are required for the running of your website/app but are processed by a build tool (perhaps to concatenate or transpile them).

In these instances it's technically true that the dependency wouldn't need to be installed in production since only the built asset would be served.  However classifying it as a development dependency would mischaracterise its contribution to the application, and could lead it to be treated with less care than it deserves (including with a looser semver range, as per the [previous example](#examples-1)).

In an ideal world where HTTP2, modern JavaScript syntax, and ES6 modules are widely supported, there would be no need to transpile or concatenate JavaScript dependencies for browsers.  Instead, they'd be loaded using `import` statements and would be directly served from their installed location. Therefore they'd unambiguously be run-time dependencies, not development dependencies. In a Node.js environment this is already possible through its native support for CommonJS `require` statements.

As such, the fact that the asset may sometimes need to be built when serving it to a browser could be considered an accident of circumstance. It shouldn't change the classification of that dependency as a run-time dependency. In this way we maintain consistency between Node.js and web applications, and provide a clear distinction between tools that are only used in the _development_ of the application, and assets that directly contribute _functionality_ to the production application.

## Configuration

Some tools, like security or static analysis tools, allow us to specify a configuration for them in either configuration files in the root of the repository (usually with `.{TOOL_NAME}rc`, `.json`, or `.js` extensions), or as an additional entry in the `package.json` file.

When using these tools, it's always preferable to include the configuration in a file than inside the `package.json`. This makes is easier to understand what tools are being used, and with what configuration, and also share those configurations between different projects.

## Publishing projects on NPM

### Naming projects

We have a springernature organisation on NPM: [https://www.npmjs.com/org/springernature](https://www.npmjs.com/org/springernature).

You must use the `springernature` [scope](https://docs.npmjs.com/getting-started/scoped-packages) when publishing packages to NPM.

```
@springernature/project-name
```

This allows us to choose meaningful names for our projects without risking collisions with other existing open source projects.

## Open source dependencies

Open source dependencies may contain security vulnerabilities, so every Node.js project must be monitored using one or more tools:

* [npm audit](https://docs.npmjs.com/cli/v8/commands/npm-audit) checks the current version of the installed packages in your project against known vulnerabilities reported on the public npm registry. If it discovers a security issue, it reports it. It's part of [npm](https://docs.npmjs.com/cli/v8/commands/npm) so it can be used on any Node.js project.
* [Snyk](https://snyk.io/) is a tool to find, fix and monitor known vulnerabilities in Node.js applications. It also supports Ruby, Java, and other languages and platforms. It's currently free for open source projects.
* [WhiteSource](https://www.whitesourcesoftware.com/) offers several tools that can be used to scan for known vulnerabilities on both open and closed source repos. You can request access to it from the cybersecurity team.

## Handling dependencies from third parties

A question that comes up from time-to-time is, "should we commit the contents of the `node_modules` directory or any selected module into version control?" On the whole we don't recommend this practice, as you should be able to install & deploy apps and their external dependencies reliably. Also some modules may be compiled differently on each host platform.

Wherever possible we suggest instead:

i) You could create a `package.json` file if not added already, where you can consider specifying package names and appropriate version numbers.

ii) For instances where you might need a specific package version or dependency, you can add in `package-lock` or `shrink-wrap` file. Consider the following cases:
- Our app requires dependency A which requires dependency B which requires dependency C which requires dependency D. There’s a vulnerability in package D, an update has been released. Using a package lock file will *prevent* the update from being used on a re-deploy, so our app will still be vulnerable, which is bad.
- Our app requires dependency A which requires dependency B which requires dependency C which requires dependency D. There’s a minor bump in dependency D that actually breaks things. Using a package lock file will *prevent* the app from breaking after a re-deploy, which is good.

iii) If you want to prevent NPM from opting for a package in a lock file, create a `.npmrc` file with following contents

```
package-lock=false
```
