---
title: "How to Create a Plugin"
linkTitle: "How to Create a Plugin"
weight: 1
description: >
  A plugin creation guide
---

# How to Create a Plugin

### Files
You will need to create two files: your plugin and your plugin configuration file. Any scripts you need added for use by your plugin will be located in the `~/PiWeatherRock/scripts` directory. For this guide, the plugin will be called `qqq`. Examples of plugins are `speedtest` and `rss`.


### Configuration File
A configutation file has the following requirements:
1. Must be located in the `~/PiWeatherRock/plugin_configs` directory.
2. Must be named ln the following way: `qqq_config.py.sample`
3. Must contain a variable named `PAUSE`
4. Each variable must have a description in the line(s) above it, which begin with a `#` and one space.
5. Limit line length to 79 characters.

### Plugin File
A plugin file has the following requirements:
1. Must be located in the root directory: `~/PiWeatherRock`
2. Must be named only with lowercase letters and/or underscores
3. Must begin with the same 39 lines as all of the other plugins (this includes the license and attribution)
4. Line 40 should be `# standard imports` followed by any imported standard libraries
5. After these standard imports will be a blank newline.
6. If any are needed: the line `# third party imports`, followed by the import statements and a blank newline.
7. If any are needed: the line `# local imports`, followed by the import statements and a blank newline.
8. Must contain a `class` with the exact name of the plugin with the first letter capitalized. Example:

`class Qqq:`

9. The `class` must contain two methods. They must be named in the following way:

`    def get_qqq(self, last_update_time):`

`    def disp_qqq(self, last_update_time):`

10. Method `get_qqq` must return the `last_update_time` when successful, or a `0` if unsuccessful
11. Method `disp_qqq` must not have a return.
12. Method must end with `pygame.display.update()`

13. Must have passed both the `flake8`<sup>a</sup> and `pyflakes`<sup>b</sup> tests. This will catch any undeclared methods, unused imports, unused variables and PEP8 formatting errors.


<sup>a</sup>: Install by executing `pip3 install pyflakes`. Pyflakes is run executing the following command from the `~/PiWeatherRock` directory:

`python3 -m pyflakes .`

<sup>b</sup>: Install by executing `pip3 install flake8`. Flake8 is run by executing the following command from the `~/PiWeatherRock` directory:

`flake8 qqq.py`