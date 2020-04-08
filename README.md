# Setup a game console in a Raspberry pi 3 
## Use your smartphone as controller for the games
This tutorial will help you to setup your raspberry pi 3 with minimum requirements in order to successfully run **Retropie** and to use as a controller your smartphone or whatever device with a browser connected to the local network.

Here is the working setup for me:
Raspberry pi with [Raspbian buster lite](https://www.raspberrypi.org/downloads/raspbian/) (the lite version requires less space on your device)

Given that you follow the instruction for installing Retropie as shown in https://retropie.org.uk/docs/First-Installation/


This work is an extension of https://retropie.org.uk/docs/Virtual-Gamepad/
I wanted to use my smartphone as controller for the game console, my upgrades are shown with a :zap:

### Install Node.js
```sudo apt-get update && sudo apt-get upgrade```

```
wget http://node-arm.herokuapp.com/node_archive_armhf.deb
sudo dpkg -i node_archive_armhf.deb
rm node_archive_armhf.deb
```
:zap: if for whatever reason is returning Error 502 bad gateway you can follow [source](https://www.raspberrypi.org/forums/viewtopic.php?t=130217)

```
curl -sL https://deb.nodesource.com/setup_4.x | sudo bash -
sudo apt-get install -y build-essential python-dev nodejs npm
```

### Update Node.js and NPM
```
sudo npm cache clean -f
sudo npm install -g n
sudo n stable
sudo npm install -g npm
```
:zap: not all version of **n** are compatible with this package be sure to specify version 9

`sudo n 9`

### Install Virtual Gamepad (Must Be Run As Root!)
we install node-virtual-gamepads in **/**
```
sudo -i
cd /
git clone https://github.com/miroof/node-virtual-gamepads
cd node-virtual-gamepads
npm install
```

:zap: There might be a dependency on a package called **forever-monitor** install it as

`npm install forever-monitor`

### Enable Virtual Gamepad on Boot

```
npm install pm2 -g
pm2 start main.js
pm2 startup
pm2 save
```

In this way everytime you turn your raspberry on an http server will show up in port 80.
Be sure to have your smartphone in the same network as the raspberry

After all this mess you will realize 2 things:
- **it's working!** but the inputs are sensitive to the **network delay**, therefore you cannot really play the games which requires fast interactions :unamused:
- i suggest you to buy a controller with usb. [link](https://www.androidcentral.com/best-raspberry-pi-controller)
