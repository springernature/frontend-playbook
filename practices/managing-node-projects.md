# Managing Node.js-based projects and dependencies

* [Specifying versions of dependencies](#specifying-versions-of-dependencies)
    * [Run-time dependencies](#run-time-dependencies)
        * [Examples](#examples)
    * [Development dependencies](#development-dependencies)
        * [Examples](#examples-1)
* [Publishing projects on NPM](#publising-projects-on-npm)
* [Dependency management tools](#dependency-management-tools)

The following guide describes how we manage package dependencies in [Springer Nature Node.js-based projects](https://github.com/springernature?utf8=%E2%9C%93&q=&type=public&language=javascript).


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
