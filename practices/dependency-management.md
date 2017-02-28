# Dependency management

The following guide describes how we manage package dependencies in our Node.js-based projects.


## Specifying versions of dependencies

As a general rule, we tend to follow a conservative approach when specifying versions for the dependencies of our packages. This helps us ensure consistency between different environments, as we can't know for sure in what environment the app is going to be running, and prevent breakage caused by major or minor updates in dependencies.

We find that the this approach strikes a good balance between the potential breakage caused by less restrictive versions and the maintenance needed when restricting the dependencies to a specific version through the use of `npm shrinkwrap` or similar tools.

We use some [dependency management tools](#dependency-management-tools) to help us keep our apps up to date when new versions of their dependencies are released.


### Run-time dependencies

[Run-time dependencies](https://docs.npmjs.com/files/package.json#dependencies) are modules that are required for your application to run, independently of the environment or mode (e.g. development vs production) used.

These are defined in the `dependencies` section of the `package.json` file.

Version numbers for run-time dependencies are defined using a tilde `~` plus a full version number in the MAJOR.MINOR.PATCH form. If the PATCH version is 0, it can be omitted.

Specifying the versions in this way ensures that:
* We don't expose the users of our modules to an unnecessary risk if one of our dependencies releases a minor update that breaks our app.
* Dependencies in early lifecycle projects (v0.MINOR.PATCH) are traditionally considered of beta quality, or undergoing heavy development, and any minor could potentially contain breaking changes. Limiting the scope to patch updates heavily reduces the chance of our app breaking.
* The behaviour when installing the dependencies is basically as predictable as possible ([Principle of least astonishment](https://en.wikipedia.org/wiki/Principle_of_least_astonishment)) without the use of npm-shrinkwrap or similar tools.

Don't use wildcards (i.e. `*`, `x`) in the package numbers or keywords like `latest`. They make the versions less clear, and predicting the outcome of installing the dependencies harder.


#### Examples

We do this:

```json
{
    "dependencies": {
        "airbrake": "~1.2.0",
        "dustmite": "~1.0.0",
        "shunter": "~4.2.1",
        "thundermole": "~1.0.3",
        "truffler": "~1.1"
    }
}
```

We _don't_ do this:
```json
{
    "dependencies": {
        "airbrake": "latest",
        "dustmite": "*",
        "shunter": "~4",
        "thundermole": "^1.0.3",
        "truffler": "~1.x"
    }
}
```

[Optional dependencies](https://docs.npmjs.com/files/package.json#optionaldependencies), if present, should also use the same format.


### Development dependencies

[Development dependencies](https://docs.npmjs.com/files/package.json#devdependencies) are required during the development, testing, or build process of the app. For example, you may include a test runner, a minifier, a bundler, etc.

These are defined in the `devDependencies` section of the `package.json` file and are not used in production environments.

Version numbers for run-time dependencies are defined using a caret `^` plus a full version number in the MAJOR.MINOR.PATCH form. If the MINOR and PATCH versions are 0, they can be omitted.


#### Examples

We do this:

```json
{
    "devDependencies": {
        "jscs": "^2",
        "mocha": "^3.1",
        "oxo": "^1.1.1"
    }
}
```

We _don't_ do this:
```json
{
    "dependencies": {
        "jscs": "latest",
        "mocha": "*",
        "toxo": "~1.1.1",
    }
}
```


## Dependency management tools

These are some of the tools that we use to help us manage the dependencies of our projects and alert us of any vulnerabilities in them:

* [Node Security Platform](https://nodesecurity.io/)
* [Snyk](https://snyk.io/)
* [Bithound](https://www.bithound.io/)
