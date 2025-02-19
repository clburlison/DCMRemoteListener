[![GitHub Contributors](https://img.shields.io/github/contributors/versx/DCMRemoteListener.svg)](https://github.com/versx/DCMRemoteListener/graphs/contributors/)
[![Discord](https://img.shields.io/discord/552003258000998401.svg?label=&logo=discord&logoColor=ffffff&color=7389D8&labelColor=6A7EC2)](https://discord.gg/zZ9h9Xa)  


# DCMRemoteListener  

## Prerequisites  
1. Install [Homebrew](https://brew.sh) if not already installed `/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install.sh)"`  
1. Update Homebrew `brew update`  
1. Uninstall previous `libimobiledevice` versions `brew uninstall --ignore-dependencies libimobiledevice`  
1. Uninstall previous `usbmuxd` versions `brew uninstall --ignore-dependencies usbmuxd`  
1. Uninstall previous `libplist` versions `brew uninstall --ignore-dependencies libplist`  
1. Install latest `usbmuxd` `brew install --HEAD usbmuxd`  
1. Install latest `libplist` `brew install --HEAD libplist`   
1. Install latest `libimobiledevice` `brew install --HEAD libimobiledevice`  
1. Install `ideviceinstaller` `brew install ideviceinstaller`  
1. Navigate to the App Store and download/install Apple Configurator 2 (AC2)<br>
1. In AC2, click on the `Apple Configurator 2` menu and choose `Install Automation Tools`<br>
1. In AC2, click on the `Apple Configurator 2` menu and choose `Preferences` > `Organization` > click on your org and choose `Export Supervision Identity` in the bottom left<br>
1. Move the .crt and .der files to the DCMRemoteListener folder and rename them to `org.crt` and `org.der`<br>

## Installation  
1. Clone repository `git clone https://github.com/versx/DCMRemoteListener`  
1. Install dependencies `npm install`  
1. Install pm2 (optional) `npm install pm2 -g`  
1. Copy example config file `cp config.example.json config.json`  
1. Fill out `config.json`  
  * Name is to identify the listener uniquely.
  * Port is the listening port, defaults to 6542.
  * Domain (i.e. `http://10.0.0.2:9991` or `https://dcm.domain.com`) is the DeviceConfigManager domain that will be sending the reboot request, otherwise set to `*` to accept from all hosts.

1. Start the bot with `pm2 start listener.js` or `node listener.js` if not using pm2  

## Config Options
```
"name" = The name you want to use for this server.
"port" = The inbound TCP port for requests.
"domain" = The domain that is allowed to send requests.
"manual_list" = True/False for creating your own JSON list of devices as device.json. See device.example.json.
"manual_ip" = True/False for adding the IP to the device.json or to allow the script to find IPs.
"use_ios_deploy" = True/False for using ios-deploy instead of cfgutil for querying devices (disables the profile command).
```

## Troubleshooting
If the cfgutil from AC2 does not list any devices when you use the `cfgutil list` command, then you may need to upgrade AC2 and reinstall the automation tools.

If the `Connection timed out` or `Connection refused` errors continuously happen for iOS 14 devices, go into Settings > Pokemon Go (at the bottom) > Toggle `Local Network` on. This will allow cURL to connect to the IPA.
