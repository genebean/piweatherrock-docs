---
title: "Getting Started"
linkTitle: "Getting Started"
weight: 1
description: >
  Installation and configuration information
---

This is guide is based on the assumption that you are using Raspbian 10 (buster). Though the code works on other platforms, the setup process has been tailored for this operating system and will not work on older versions. You can verify what version of Raspbian you have by running this command:

```bash
cat /etc/os-release
```

## Prerequisites

Before setting up PiWeatherRock you need to setup automatic logins to the desktop. Do this by running the command `sudo raspi-config` in a terminal. When the program opens select "Boot Options" > "Desktop / CLI" > "Desktop Autologin". Select finish and then reboot if prompted.

The next thing you need to do is go to https://darksky.net/dev and get an API key. You can make up to 1,000 API calls per day without paying, or even providing payment info.

In addition to your API key, you will also need your latitude and longitude. https://gps-coordinates.org seems to work well for this but I prefer to use the compass app on my iPhone.

## Installation and setup

Clone the PiWeatherRock repository to your to your home directory:

```bash
git clone https://github.com/genebean/PiWeatherRock.git /home/pi/PiWeatherRock
```

Once you have cloned the repository, `cd` into it and create your initial config file:

```bash
cd /home/pi/PiWeatherRock
cp config.py.sample config.py
```

Edit `config.py` and adjust the values based on your preferences.

With the config file edited you are ready to run the install script by providing it with the name you'd like your Pi to have. For example, to name your Pi `mylittlepi` you'd do this:

> If you have already renamed your Pi its fine to enter the current name here

```bash
sudo ./install.sh mylittlepi
```

This will execute the [install.sh](https://github.com/genebean/PiWeatherRock/blob/master/install.sh) which will do some initial prep work and then use Puppet to configure everything else by applying [setup.pp](https://github.com/genebean/PiWeatherRock/blob/master/setup.pp).

When this finishes you will have a new systemd service named [PiWeatherRock.service](PiWeatherRock.service) that automatically starts up. You can check the status of the service by running `sudo systemctl status PiWeatherRock`.
