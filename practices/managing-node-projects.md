# Managing Node.js-based projects and dependencies

- [Installing dependencies](#installing-dependencies)
  - [Using the right version of node](#using-the-right-version-of-node)
  - [How to specify the version of node to use](#how-to-specify-the-version-of-node-to-use)
    - [`nvm` usage](#nvm-usage)
    - [Automatically running `nvm use`](#automatically-running-nvm-use)
  - [Should I check in `package-lock.json` to version control?](#should-i-check-in-package-lockjson-to-version-control)
  - [Managing changes to the `package-lock.json` file](#managing-changes-to-the-package-lockjson-file)
- [Specifying versions of dependencies](#specifying-versions-of-dependencies)
  - [Run-time dependencies](#run-time-dependencies)
    - [Examples](#examples)
  - [Development dependencies](#development-dependencies)
    - [Examples](#examples-1)
  - [Classifying "built" run-time dependencies](#classifying-built-run-time-dependencies)
- [Configuration](#configuration)
- [Publishing projects on NPM](#publishing-projects-on-npm)
  - [Naming projects](#naming-projects)
- [Dependency management tools](#dependency-management-tools)
- [Handling dependencies from third parties](#handling-dependencies-from-third-parties)

The following guide describes how we use node and manage package dependencies in [Springer Nature Node.js-based projects](https://github.com/springernature?utf8=%E2%9C%93&q=&type=public&language=javascript).


## Installing dependencies

There are two methods for installing node dependencies: `npm install` and `npm ci`.

`npm install` is the most common method, but it doesn't guarantee reproducible/consistent builds. npm can install varying versions of dependencies, according to [semantic versioning](https://docs.npmjs.com/files/package.json#dependencies) and the version of node used when installing. `npm install` will create a `package-lock.json` file describing the complete dependency graph and specifying exact versions of all the dependencies installed.

Note that if a `package-lock.json` is present **`npm install` will not use it** as the source of authority for what to install.

This is the method we recommend for installing dependencies when authoring node _libraries_.

`npm ci` however installs the complete dependency graph exactly as specified in the `package-lock.json` file, and so guarantees reproducible/consistent builds. This helps reduce "but it works on my machine" issues and is suitable for CI/CD environments (as the name implies).

[`npm ci` is also much quicker than `npm install`](https://docs.npmjs.com/cli/ci.html#description) if the `./node_modules` directory is not present (such as in a CI environment).

It is the method recommended for installing dependencies when authoring node _applications_.

### Using the right version of node

When authoring libraries you are probably supporting multiple versions of node, so it not required to use a specific version when installing (as long as the version is supported by your library).

When authoring node applications, and therefore using `npm ci`, it is important to specify a version of node to use. This is because the `package-lock.json` file will reflect the version of node used when the `package-lock.json` file was created. If you don't use the same version of node when running `npm ci`, the versions of dependencies specified in the `package-lock.json` may be incompatible with the version of node you are currently using, and you may get installation errors.

### How to specify the version of node to use

There are two main ways of doing this, and you're encouraged to do both.

1. The [`engines`](https://docs.npmjs.com/files/package.json#engines) field in `package.json`:
     * `engines` is important if authoring libraries. Let's assume we're using a different version of node to that specified in `engines` field for package `foo`.
     When running `npm install` to install `foo`'s dependencies, `npm` will warn about the problem.
     When `npm install`ing a package _which depends on_ `foo`, `npm` will warn and error.
     * Some deployment environments also respect it.
     * It makes compatibility requirements explicit to developers working on your application.
2. Using an `.nvmrc` file:
     * An `.nvmrc` file is a configuration file for `nvm` ([Node Version Manager](https://github.com/creationix/nvm)).
     Use of `nvm` is strongly encouraged as an application author, as it enables you to specify to other developers what versions of node they should be using when running your app.
     * Your application should include an [`.nvmrc` file](https://github.com/creationix/nvm#nvmrc) in the root directory of the project to specify which version(s) of node are compatible.
     * It also is required for proper `npm ci` usage, as explained above.
     * It also makes life much easier when working on multiple node projects locally that require different versions of node.

#### `nvm` usage

When you check out a project, you should first run `nvm use` before `npm ci` to ensure you're running on the same version of node the project expects. Additionally [Travis respects `.nvmrc` files](https://docs.travis-ci.com/user/languages/javascript-with-nodejs/#specifying-nodejs-versions-using-nvmrc), so using one will simplify your Travis configuration and help other developers avoid mistakes.

#### Automatically running `nvm use`

As mentioned above, it is important to run `nvm use` before `npm ci`. But this is a thing that's easy to forget!

To avoid forgetting, there are useful shell extensions ([zsh](https://github.com/creationix/nvm#calling-nvm-use-automatically-in-a-directory-with-a-nvmrc-file),
[bash](https://stackoverflow.com/questions/23556330/run-nvm-use-automatically-every-time-theres-a-nvmrc-file-on-the-directory))
which run `nvm` and switch node versions for you when `cd`-ing into a directory. Well worth installing.

### Should I check in `package-lock.json` to version control?

Yes. There are two main reasons:

1. Predictable builds, as discussed above.
1. Dependency analysis tools (such as `npm audit`, GitHub Security Alerts and `snyk`) can spot insecure dependencies anywhere in the dependency tree by analysing the `package-lock.json` file. These tools can force patch version updates of insecure dependencies in the tree, without waiting for third-party package maintainers to release new packages with updated dependencies. This wouldn't be possible without a `package-lock.json` and is a huge benefit.

The downside is it requires all developers to use `nvm` and `npm ci` to install dependencies, otherwise there will be constant conflicts in the `package-lock.json` file.

### Managing changes to the `package-lock.json` file

Firstly, bear in mind machine-generated files should not be hand-edited, and `package-lock.json` is no exception.

Secondly, if you are seeing unexpected merge conflicts in `package-lock.json` it can be a symptom of someone using `npm install` instead of `npm ci`. Speak to the developer and see if they are having trouble.

Additionally, when updating your application its strongly recommend to keep `package-lock.json` changes as a result of `npm update` or `npm audit fix` in a separate PR to other changes to the application. This helps by making your PRs easier to review.

## Specifying versions of dependencies

As a general rule, we tend to follow a conservative approach when specifying versions for the dependencies of our packages. We only allow PATCH version ranges for [run-time dependencies](#run-time-dependencies) and MINOR + PATCH version ranges for [dev dependencies](#development-dependencies). This helps us ensure consistency between different environments, as we can't know for sure in what environment the app is going to be running, and prevent breakage caused by major or minor updates in dependencies.

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

Version numbers for run-time dependencies are defined using a caret `^` plus a full version number in the `MAJOR.MINOR.PATCH` form. For a package version specified as `^2.3.4` this means that all releases from `2.3.4` (inclusive) up to, but not including `3.0.0` are acceptable.

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

This allows us to choose meanunful names for our projects without risking collisions with other existing open source projects.


## Dependency management tools

[Snyk](https://snyk.io/) is a tool to find, fix and monitor known vulnerabilities in Node.js applications. It also supports Ruby, Java, and other languages and platforms.

Snyk not only provides alerts when a new vulnerability is detected in one of the dependencies that we use, but also remediation options.

[Using components with known vulnerabilities caused 24% of the top 50 breaches](https://snyk.io/blog/owasp-top-10-breaches/). Keeping dependencies up-to-date is therefore crucial to maintain our standards of security.

Every node.js project must be added to the Springer Nature organisation in Snyk so it can be monitored for security vulnerabilities.

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
