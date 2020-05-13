---
title: "Install Option 2"
linkTitle: "Option 2"
weight: 10
resources:
- src: "Puppet-Forge-screen-shot.png"
  params:
    byline: "Puppet Forge May 2020"
---

Let me start with a warning: this option is more complicated and more likely to result in typos that cause things to not work as intended. It is also a transcription of what I am telling software to do automatically in Option 1. I will try to keep this up to date but strongly encourage you to use the process outlined above.

This method can be broken down into the following sections:

1. log into your Pi via ssh
2. install prerequisite software via `apt`
3. install prerequisite software via `pip3`
4. install PiWeatherRock via `pip3`
5. create / edit configuration files needed by PiWeatherRock
6. create systemd services
7. run the configuration updating utility
8. start the webconfig service
9. add an API key
10. start the main service

First off, get connected to your Pi via ssh. The process for this will vary based on your operating system but generally equates to using Terminal or iTerm2 on macOS, PuTTY on Windows, or whatever terminal your Linux distro provides.

Next, you will need to have a look at [`install.pp`](https://github.com/genebean/genebean-piweatherrock/blob/master/manifests/install.pp) from the Puppet module used in Option 1 and find the lists of packages entitled `$_main_packages` and `$_piweatherrock_packages`. Each item in those lists will need to be installed via `sudo apt-get install --no-install-recommends <name of package>`. Additionally, you will want to install `realvnc-vnc-server` in the same way.

Next, you will need to run `sudo pip3 install setuptools wheel` as they are prerequisites to being able to install PiWeatherRock.

Next, have a look at the reference docs for the module on the Puppet Forge at [https://forge.puppet.com/genebean/piweatherrock/reference](https://forge.puppet.com/genebean/piweatherrock/reference) and find the section that starts with `piweatherrock_version`. Make note of the value in that section next to `Default value:` if it's anything other than `latest` as you'll need it in the next step.

To install PiWeatherRock you will run one of the following two commands based on what you observed in the last step:

- If the value was `latest` then you will want to run `sudo pip3 install piweatherrock`
- If the value was anything else you will want to run a variation of the install command above that includes the value. For example, if the value was `X.Y.Z.dev0` the install command would be `sudo pip3 install piweatherrock==X.Y.Z.dev0`.

Next, create `/home/pi/bin` and then crate a file in it named `/home/pi/bin/xhost.sh` with the following content and permissions of `0755`:

```bash
#!/bin/bash
xhost +
```

Next run the following command to tell LightDM to use the file you just created:

```bash
sed -i 's|#display-setup-script=|display-setup-script=/home/pi/bin/xhost.sh|' /etc/lightdm/lightdm.conf
```

Next, create `/etc/systemd/system/PiWeatherRock.service` and `/etc/systemd/system/PiWeatherRockConfig.service` based on what is in the templates listed at [https://github.com/genebean/genebean-piweatherrock/tree/master/templates](https://github.com/genebean/genebean-piweatherrock/tree/master/templates). Be advised that any time you see something formatted like `<%= $config_file %>` that it is referencing a variable. The values that replace that can be found in the sections that start with `systemd::unit_file` in [https://github.com/genebean/genebean-piweatherrock/blob/master/manifests/service.pp](https://github.com/genebean/genebean-piweatherrock/blob/master/manifests/service.pp).

Next up is running the configuration utility.

```bash
export config_file='/home/pi/piweatherrock-config.json'
export sample_config_file='/usr/local/lib/python3.7/dist-packages/piweatherrock/config.json-sample'
/usr/local/bin/pwr-config-upgrade -c ${config_file} -s ${sample_config_file}
```

#### Start services

Now, run `sudo systemctl start PiWeatherRockConfig`. You should now be able to go to port 8888 of your Pi in a web browser. From there, enter an API key and then return to your terminal and run `sudo systemctl start PiWeatherRock`.

If all is well you will see PiWeatherRock start running on the monitor connected to your Pi. If not, see the logs referenced at the end of Option 1 above or reach out on [Gitter](https://gitter.im/PiWeatherRock/community).
