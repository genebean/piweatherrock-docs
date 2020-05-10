---
title: "Getting Updates"
linkTitle: "Getting Updates"
weight: 2
description: >
  How to get the latest version of PiWeatherRock
---

## What's changed

[CHANGELOG.md](https://github.com/genebean/PiWeatherRock/blob/master/CHANGELOG.md) is maintained in the PiWeatherRock repository and lists the notable changes from one version to the next.

## Migrating

First, if you installed when the process included using `git clone` be sure you have run the migration documented at [Migrating to the PyPI version](migration-to-pypi/).

## General update process

The recommended way to to upgrade is to run these two commands on your Pi either locally or via SSH:

```bash
sudo puppet module upgrade genebean-piweatherrock
sudo puppet apply -e "include piweatherrock"
```
