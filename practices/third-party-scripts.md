# Third party scripts

Whenever possible, we make use of a tag managers in order to easily manage the scripts being included on a page. We currently use:

* [Ensighten](https://manage.ensighten.com)
* [Google Tag Manager](https://tagmanager.google.com)

for this purpose.

## Third party scripts policy

Tag managers make it very easy for anyone to add any scripts to a page. We publish a huge amount of content so it's easy to publish a tag on more sites than necessary, or to not be aware of its performance impact.

Most of these are taken from Andrew Welch's "[Tags Gone Wild! Managing Tag Managers](https://nystudio107.com/blog/tags-gone-wild)".

* Every tag should have an owner, in terms of a person who takes responsibility for that tag.
* Every tag should be documented, stating what it does, and justifying its existence.
* Tags should appear only on the pages where they are actually needed, not globally on every page on the website.
* Tags that coincide with a marketing campaign should be set up to expire at an appropriate date.
* Tags should be audited on a regular basis, and pruned back regularly.

We carry regular tests using tools like [WebPagetest](https://www.webpagetest.org/) and [SpeedCurve](https://www.speedcurve.org/) to ensure that performance is not affected by these scripts.
