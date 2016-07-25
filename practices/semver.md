# SemVer

## What is SemVer

SemVer is a way of versioning software in the format of MAJOR.MINOR.PATCH:

 - MAJOR version when you make breaking changes,
 - MINOR version when you add functionality in a backwards-compatible manner for any specific MAJOR version, and
 - PATCH version when you make backwards-compatible bug fixes to any specific MAJOR.MINOR version.

This means that any time you release a new MAJOR release, the minor and patch values reset to 0, and the same is true of the patch value when making a MINOR release.

For more information about how SemVer is defined, please see: http://semver.org/

## Why we use SemVer

SemVer allows us to keep a consistent numbering scheme to ensure that going forward we can maintain compatibility with all system and platform components.  It also allows us to upgrade dependencies with the confidence that things won’t break.

SemVer enables us to ensure that once something is committed we can be confident that any version remains unique.

## Common concerns

### How can I trust that things aren’t going to break with a minor or patch release update?

Like any practice, SemVer can be let down by people not using it correctly (like releasing a breaking change under a minor version rather than a major).  It’s the responsibility of the person upgrading to ensure that the upgrade is appropriate and compatible.

### The version number is getting really big really quickly!

When a piece of software under heavy development many major/minor releases may happen in quick succession, so your version might start to look like 23.2.0 or 3.34.1.  THAT’S OKAY!  If that’s a true representation of what has happened in the code, then it’s appropriate that the version number reflects that.  

What _might_ be a worry is if your version looked like 2.1.45 - did you really release 45 patches/bug fixes in a row without adding any new features?

## Find out more:
- Canonical source of info: http://semver.org/
- [How we version and release our open-source software](https://github.com/springernature/shunter/blob/master/docs/developer-guide.md#versioning)
- More reading: https://abdulapopoola.com/2015/10/26/what-is-semver/
