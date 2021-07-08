---
title: "How to Create a Plugin"
linkTitle: "How to Create a Plugin"
weight: 1
description: >
  A plugin creation guide
---

This is a guide on how to create a plugin for PiWeatherRock. We welcome all contributions. Each plugin needs both data and a visual representation of that data. If this is your first time contributing to a project on GitHub, read through [this great info](https://piweatherrock.technicalissues.us/docs/contribution-guidelines/). If you still have questions, reach out on [gitter](https://gitter.im/PiWeatherRock/community)

## Files
You will need to create two files: your plugin and your plugin configuration file. Any scripts you need added for use by your plugin will be located in the `~/PiWeatherRock/scripts` directory. For this guide, the plugin will be called `qqq`. Examples of plugins are `speedtest` and `rss`.


## Configuration File
A configutation file has the following requirements:
1. Must be located in the `~/PiWeatherRock/plugin_configs` directory.
2. Must be named ln the following way: `qqq_config.py.sample`
3. Must contain a variable named `PAUSE`
4. Each variable must have a description in the line(s) above it, which begin with a `#` and one space.
5. Limit line length to 79 characters.

## Plugin File
A plugin file has the following requirements:
1. Must be located in the root directory: `~/PiWeatherRock`
2. Must be named only with lowercase letters and/or underscores. Example: `qqq.py`
3. Must begin with the same 39 lines as all of the other plugins (this includes the license and attribution)
4. Line 40 should be `# standard imports` followed by any imported standard libraries
5. After these standard imports will be a blank newline.
6. If any are needed: the line `# third party imports`, followed by the import statements and a blank newline.
7. If any are needed: the line `# local imports`, followed by the import statements and a blank newline.
8. Must contain a `class` with the exact name of the plugin with the first letter capitalized. Example: `class Qqq:`
9. The `class Qqq` must contain the following meathod: `def get_qqq(self, last_update_time):`
9. The `class Qqq` must contain the following meathod: `def disp_qqq(self, last_update_time):`
11. Method `get_qqq` must return the `last_update_time` when successful.
12. Method `get_qqq` must return `0` if unsuccessful on it's initial call.
13. Method `get_qqq` must return the `last_update_time` + some `integer` when unsuccessful after initial call. The integer represents the number of seconds to wait before attempting the update again.
14. Method `disp_qqq` must not have a return.
15. Method `disp_qqq` must end with `pygame.display.update()`
16. Plugin file `qqq.py` must have passed both the `flake8` <sup>a</sup> and `pyflakes` <sup>b</sup> tests. These tests will catch any undeclared methods, unused imports, unused variables and PEP8 formatting errors.


<sup>a</sup>: Install by executing `pip3 install pyflakes`. Pyflakes is run executing the following command from the `~/PiWeatherRock` directory: `python3 -m pyflakes .`

<sup>b</sup>: Install by executing `pip3 install flake8`. Flake8 is run by executing the following command from the `~/PiWeatherRock` directory: `flake8 qqq.py`
