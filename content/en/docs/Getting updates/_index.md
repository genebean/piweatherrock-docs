---
title: "Getting Updates"
linkTitle: "Getting Updates"
weight: 2
description: >
  How to get the latest version of PiWeatherRock
---

[CHANGELOG.md](https://github.com/genebean/PiWeatherRock/blob/master/CHANGELOG.md) is maintained in the PiWeatherRock repository and lists the notable changes from one version to the next. If you are on a version newer than 1.3.0 you will have a copy of the change log in your PiWeatherRock directory. The newest numbered version in that file should correspond to the version you are running.

## Upgrading from before v1.3.0

Version 1.3.0 introduced the web-based configuration page. The update process above will take care of migrating your settings so there is nothing extra that should be need. Please see the getting started page for more info.

## General update process

Run the commands below to update your copy of PiWeatherRock:

> Note that this code block includes more than just the command you type into your terminal. The command is just the bit directly after the `$`

```bash
pi@rock:~/PiWeatherRock $ git pull
# you should see some output from git here if there are any updates

pi@rock:~/PiWeatherRock $ sudo puppet apply setup.pp
# below is a sample of the type of output you may see
Notice: Compiled catalog for rock in environment production in 0.81 seconds
Notice: /Stage[main]/Main/Python::Pip[darkskylib]/Exec[pip_install_darkskylib]/returns: executed successfully
Notice: /Stage[main]/Main/Service[PiWeatherRock.service]: Triggered 'refresh' from 1 event
Notice: Applied catalog in 115.65 seconds
```
