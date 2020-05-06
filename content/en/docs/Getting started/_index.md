---
title: "Getting Started"
linkTitle: "Getting Started"
weight: 1
description: >
  Installation and configuration information
---

{{% alert title="Notice" color="warning" %}}
On March 30, 2020 an announcement was posted to the [Dark Sky Blog](https://blog.darksky.net) stating that they have
been acquired by Apple. The announcement went on to say that they are no longer accepting new requests for API access and that they
will be shutting the API down at the end of 2021.

This unfortunate bit of news isn't the end of this project... I've been here before. This just means that I will have to do a third
API migration. Work related to this, and suggestions on what API to use, are being tracked in
[issue 48](https://github.com/genebean/PiWeatherRock/issues/48) of the project's GitHub repo.
{{% /alert %}}

This is guide is based on the assumption that you are using Raspbian 10 (buster). Though the code works on other platforms, the setup process has been tailored for this operating system and will not work on older versions. You can verify what version of Raspbian you have by running this command:

```bash
cat /etc/os-release
```

## Prerequisites

Before setting up PiWeatherRock you need to setup automatic logins to the desktop. Do this by running the command `sudo raspi-config` in a terminal. When the program opens select "Boot Options" > "Desktop / CLI" > "Desktop Autologin". Select finish and then reboot if prompted. You will also need to be sure and complete the configuration required in the popup that is shown on login.

~~The next thing you need to do is go to https://darksky.net/dev and get an API key. You can make up to 1,000 API calls per day without paying, or even providing payment info.~~ *This will get updated soon.*

In addition to your API key, you will also need your latitude and longitude. https://gps-coordinates.org seems to work well for this but I prefer to use the compass app on my iPhone.

## Installation and setup

Clone the PiWeatherRock repository to your to your home directory:

```bash
git clone https://github.com/genebean/PiWeatherRock.git /home/pi/PiWeatherRock
```

> The next step is new and will only be needed during the transitional period between now and when the new version is completed.

Once you have cloned the repository, `cd` into it and checkout the last stable version:

```bash
$ cd /home/pi/PiWeatherRock

$ git fetch --all --tags
Fetching origin

$ git checkout tags/1.3.0
Note: switching to 'tags/1.3.0'.
# a bunch of output will show here... disregard it.

$ git status
HEAD detached at 1.3.0
nothing to commit, working tree clean
```

So long as you see the `HEAD detached at 1.3.0` line after the last command everything has worked as expected.

The next step is to run the install script. You will need to provide it with the name you'd like your Pi to have. For example, to name your Pi `mylittlepi` you'd do this:

> If you have already renamed your Pi its fine to enter the current name here

```bash
sudo ./install.sh mylittlepi
```

This will execute the [install.sh](https://github.com/genebean/PiWeatherRock/blob/master/install.sh) which will do some initial prep work and then use Puppet to configure everything else by applying [setup.pp](https://github.com/genebean/PiWeatherRock/blob/master/setup.pp).

When this finishes you will have two new systemd services

- [PiWeatherRockConfig.service](https://github.com/genebean/PiWeatherRock/blob/master/PiWeatherRockConfig.service)
- [PiWeatherRock.service](https://github.com/genebean/PiWeatherRock/blob/master/PiWeatherRock.service)

The first one facilitates configuring PiWeatherRock by navigating to port 8888 of your Pi. I suggest doing this from a computer other than your Pi to avoid issues. If you named your Pi `mylittlepi` then you would go to [http://mylittlepi.local:8888](http://mylittlepi.local:8888).

You can check the status of the configuration service by running `sudo systemctl status PiWeatherRockConfig`. You can check the status of the main application by running `sudo systemctl status PiWeatherRock`.
