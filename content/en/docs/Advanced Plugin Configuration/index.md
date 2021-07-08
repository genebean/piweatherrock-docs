---
title: "Advanced Plugin Configururation"
linkTitle: "Advanced Plugin Configururation"
weight: 1
description: >
  plugin-specific configuration information
---

# Speedtest

This is a guide on how to run speedtests periodically on a different machine and feed the results to PiWeatherRock.

## Preamble:
Older and underpowered Raspberry Pi's have difficulty keeping up with faster and faster network speeds provided by modern ISPs. If you are considering using the `speedtest` plugin and running the tests on the Pi, it's recommended that you perform speedtests on both your Pi and on a different machine that is known to get the full speeds provided. Compare the results, and if you decide they are close enough, then running the speedtests on the Pi is an option. If not, you can setup a different machine to do the speedtests and then feed that information to PiWeatherRock for display.


### Notes:
- For best results, you'll want to run speedtests on a computer/server that is on 24/7. In this guide we will call this machine 'the server'.
- Make sure that PiWeatherRock is not running while we make the necessary changes. Execute `sudo systemctl stop PiWeatherRock` from terminal on the Pi to stop it.

## Installing on Windows machine
Pending future update
## Installing on GNU/Linux or macOS machine

### PREP:
1. We'll need CURL installed.
2. On macOS, in a terminal, execute the following commands:

`ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)" < /dev/null 2> /dev/null`

`brew install curl`

3. On Debian-based GNU/Linux, in a terminal, execute the following command:

`sudo apt install curl`

### PART 1: Prepare the server for speedtest script, for SSH connection and get other basic information
1. Open a terminal on the server
2. Create a directory needed for PART 2 by executing the following command:

`mkdir .ssh`

3. Get the server hostname for PART 2 by executing the following command:

`hostname -f` 

or simply

`hostname`

4. Create a directory for the speedtest application and move to that directory by executing the following commands:

`mkdir .speedtest`

`cd .speedtest`

5. Create a directory for the sppedtest results by executing the following commands:

`mkdir results`

`mkdir results/queue`

`mkdir results/archive`

6. Download the speedtest application by executing the following command:

`curl -Lo speedtest-cli https://raw.githubusercontent.com/sivel/speedtest-cli/master/speedtest.py
chmod +x speedtest-cli`

7. Create the speedtest script by executing the following commands:

`echo '#!/bin/bash' >> speedtest.sh`

`echo '~/.speedtest/speedtest-cli --json > ~/.speedtest/results/queue/$(date +%s).json' >> speedtest.sh`

8. Let's find out where the application `bash` is located (for step 11) by executing the following commmand:

`which bash`

9. Now, we'll set the script to run periodically. Execute the following command:

`crontab -e`

10. If this is your first time using cron, you may be prompted to choose your default text editor. Choose 'nano', as it is easier for beginners.
11. The first line below will run the speedtest every 20 minutes. The seond line below will run the speedtest every 2 hours (at 23 minutes past the hour). Choose a line and edit it for your desired test interval. Replace `/usr/bin/bash` with the output from step 8. Then use down arrow to move the cursor to the very last line and paste the edited line below into the terminal screen:

`*/20 * * * * /usr/bin/bash ~/.speedtest/speedtest.sh`

`23 */2 * * * /usr/bin/bash ~/.speedtest/speedtest.sh`

12. Type `ctrl` + 'x' to exit. Type 'Y' to save. Type `return/enter` to confirm the filename.
13. We'll need at least one speedtest result before starting PiWeatherRock. If the interval you input above is fairly long, you can run a speedtest right now by executing the following command:

`bash ~/.speedtest/speedtest.sh`

### PART 2: Setup RSA-key-based SSH connection

#### NOTE:
*PART 2 is optional.* If you skip PART 2, you'll have to manually mount the server's speedtest directory after every reboot and enter the server's password when prompted. If you do this, add 'no_auto' between 'defaults' and 'allow_other' in PART 3, step 2.

1. On the Pi, open a terminal and execute the following command (when prompted, just hit `return/enter` unless you are familiar with advanced RSA key creation):

`ssh-keygen -t rsa`

2. Add the key to the server (substitute your server username and hostname) by executing the following command:

`cat .ssh/id_rsa.pub | ssh SERVER_USERNAME@SERVER_HOST_NAME 'cat >> .ssh/authorized_keys'`

3. You will be prompted to enter the password used to login to the server OS with that username.
4. Protect the key (substitute your server username and hostname) by executing the following command:

`ssh SERVER_USERNAME@SERVER_HOST_NAME "chmod 700 .ssh; chmod 640 .ssh/authorized_keys"`

5. Test the SSH connection (substitute your server username and hostname) by executing the following command:

`ssh SERVER_USERNAME@SERVER_HOST_NAME`

6. You should now be logged into the server. Type 'exit', then `enter/return` to close the connection.

### PART 3: Automatically make the speedtest results available to the Pi when the Pi starts up.
1. Open a terminal on your Pi
2. Allow the Pi to access the speedtest results (substitute your server username and hostname - make sure to keep the '#' before the server name) by executing the following command:

`sudo su -c "echo 'sshfs#SERVER_USERNAME@SERVER_HOST_NAME:~/.speedtest/results/ /home/pi/PiWeatherRock/speedtest/ fuse defaults,allow_other 0 0' >> /etc/fstab"`

3. NOTE: If you have run speedtests using your Pi already, you'll need to either delete the `~/PiWeatherRock/speedtest` directory or move it somewhere else.
4. Create the directory for the speedtest files by executing the following command:

`mkdir /home/pi/PiWeatherRock/speedtest/`

5. The speedtest files from the server will be available When the Pi is restarted. To make them available now, execute the following command:

`sudo mount /home/pi/PiWeatherRock/speedtest`

### PART 4: Edit the PiWeatherRock config files.
1. On the Pi open `config.py` for editing.
2. If there is a variable called `PLUGINS`, add 'speedtest' to the list. Example:

`PLUGINS = ['daily', 'hourly', 'speedtest']`

3. If there is no variable called `PLUGINS`, you are using an outdated version of PiWeatherRock. First upgrade before moving on.
4. Open `speedtest_config.py.sample` from the `plugin_configs` directory.
5. Fill in the options with your information. Make sure `SPEEDTEST_ON_PI = False`
6. Rename `speedtest_config.py.sample` to `speedtest_config.py`
7. Start PiWeatherRock by executing the following command:

`sudo systemctl start PiWeatherRock`

