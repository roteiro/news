# Nextcloud News app

## About this fork
This fork enables you to use the awesome [Nextcloud News App](https://github.com/nextcloud/news) with 32-bit hardware/software (e.g. NextCloudPi). 
32-bit support was removed from the original Nexctloud News App with Release 16.0.0. This fork restores 32-bit compability, since my system is still running on 32-bit software and a lot of systems out there have the same requirements.

Use this fork at your own risk and only if you know what you are doing!

Installation of the app needs to be done manually, the procedure is described in [INSTALL.md](./INSTALL.md).

The idea was taken from [PR #1337](https://github.com/nextcloud/news/pull/1337). A detailed discussion on the reasoning for removing 32-bit support from the original app can be found [here](https://github.com/nextcloud/news/issues/1423).

The remainder of this README is identical to the README of the original News app.
**********************************************************************************

**We need help with the frontend, check the issue tracker if you are interested!**

![Release status](https://github.com/nextcloud/news/workflows/Build%20and%20publish%20app%20release/badge.svg) ![Integration Tests](https://github.com/nextcloud/news/workflows/Integration%20Tests/badge.svg) ![Frontend tests](https://github.com/nextcloud/news/workflows/Frontend%20tests/badge.svg) [![Code coverage](https://img.shields.io/codecov/c/github/nextcloud/news.svg?style=flat)](https://codecov.io/gh/nextcloud/news/)

The News app is an RSS/Atom feed aggregator. It offers a [RESTful API](https://nextcloud.github.io/news/developer/#apis) for app developers. The source code is [available on GitHub](https://github.com/nextcloud/news)

## Documentation
The documentation can be found [here](https://nextcloud.github.io/news/), the source of the documentation is on [GitHub](https://github.com/nextcloud/news/blob/master/docs)

## Bugs
Please read the [appropriate section in the contributing notices](https://github.com/nextcloud/news/blob/master/CONTRIBUTING.md#issues)

## Updating Notices
To receive notifications when a new News app version was released, simply add the following Atom feed in your currently installed News app:

    https://github.com/nextcloud/news/releases.atom

## Screenshots
![](https://raw.githubusercontent.com/nextcloud/news/master/screenshots/1.png)

## Maintainers

* [Benjamin Brahmer](https://github.com/Grotax)
* [Sean Molenaar](https://github.com/SMillerDev)

### Special thanks to the Feed-IO library
Please consider donating to the developer of the RSS parser that powers the Nextcloud News App: [https://github.com/sponsors/alexdebril](https://github.com/sponsors/alexdebril)
