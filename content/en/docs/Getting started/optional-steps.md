---
title: "Optional Steps"
linkTitle: "Optional Steps"
weight: 2
description: >
  Optional additional steps to supplement the default setup.
---

## Non-stock GUI

[https://forge.puppet.com/genebean/piweatherrock](https://forge.puppet.com/genebean/piweatherrock) contains some optional settings that may be useful if you started with Raspbian Lite or simply prefer the [awesome window manager](https://awesomewm.org/). You can install it by running the following command on your Pi post-installation:

```bash
sudo puppet apply -e "class { 'piweatherrock': enable_awesome_desktop => true, }"
```

## Cron job for Puppet

Running the command below will tell puppet to keep things in line every 30 minutes. See https://crontab.guru/ for examples of how you could adjust the interval.

```bash
puppet resource cron 'run puppet' \
ensure=present \
command='/usr/bin/sudo /usr/bin/puppet apply -e "include piweatherrock"' \
minute='*/30'
```
