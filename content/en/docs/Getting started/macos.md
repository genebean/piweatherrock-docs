---
title: "PiWeatherRock on macOS"
linkTitle: "macOS"
weight: 1
description: >
  Running PiWeatherRock on macOS
---

One of the other operating systems this code works on is macOS. I have not yet gone through the effort of creating services to make things automatic like it is on Linux but that doesn't mean you can't still enjoy using your laptop or iMac as a fancy weather rock.

Installing roughly breaks down to these steps:

Install [Homebrew](https://brew.sh/) and then run these commands:

```bash
brew install python
pip3 install setuptools wheel
pip3 install piweatherrock
```

That will get it installed. Next, run this chain of commands to create or update your configuration file:

```bash
/usr/local/bin/pwr-config-upgrade -s "$(pip3 show piweatherrock |grep '^Location' |cut -d ' ' -f2)/piweatherrock/config.json-sample" -c ~/piweatherrock-config.json
```

With a config file in place, temporarily start up the web-based configuration utility by running `/usr/local/bin/pwr-webconfig -c ~/piweatherrock-config.json` and then opening [http://localhost:8888](http://localhost:8888) in a web browser. Enter your API key and location information on that page. Once you are finished you can press the control key and the letter c at the same time in your terminal to kill the utility.

Now you should be able to run `/usr/local/bin/pwr-ui -c ~/piweatherrock-config.json` in your terminal to get the program started. If you changed fullscreen to false on the config page you will also be able to resize it and use it kinda like a widget or put it on a second monitor or whatever you like.
