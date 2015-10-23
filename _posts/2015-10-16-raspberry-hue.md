---
layout: blog
title: Raspberry&hue
category: blog
tags: [Raspberry, hue]
summary: Raspberry connect with hue
image: https://scontent.xx.fbcdn.net/hphotos-xat1/v/t34.0-12/11997016_10153667976625956_706060187_n.jpg?oh=4a6292eb1c73b03a727e89e2f7e93407&oe=55F89B44
---

# Check network connecting

* Using the following command:
         arp-scan -I スキャンを行うネットワークアダプタ(eth0など) -l
* Using ifconfig to specify network_adapter

```
nifty-5080:~ sci01445$ sudo arp-scan --interface en6 -l
Interface: en6, datalink type: EN10MB (Ethernet)
Starting arp-scan 1.9 with 256 hosts (http://www.nta-monitor.com/tools/arp-scan/)
172.28.192.207	00:17:88:19:15:8f	Philips Lighting BV
172.28.192.208	b8:27:eb:eb:d1:79	Raspberry Pi Foundation
```

# Raspberryの準備

* Internet接続(WIFI)
        sudo wpa_passphrase dgnet faat3268 | sudo tee -a /etc/wpa_supplicant/wpa_supplicant.conf
* 再起動
        sudo reboot
* shutdownをする時はこちらのコマンドはいいですね！
        sudo shutdown -H now
* 接続by SSH
       ssh pi@xxx.xxx.xxx.xxx
       ls home/pi/duong_raspi/
* Copy file from MAC to Raspberry
        scp /destination/filename pi@19X.XXX.XXX.XXX:destination/path (substituting raspberrypi.local for your device’s IP address)
参考: http://thomasloughlin.com/how-to-transfer-files-from-a-mac-or-pc-onto-a-raspberry-pi/
        scp hue_test.js root@172.28.192.189:/home/pi/hue_raspi

# Hue

* API: http://www.developers.meethue.com/users/thuydg
* https://my.meethue.com/ja-jp/
* bridge information: https://www.meethue.com/en-us/user/bridge
* settings:

```
Ethernet MAC Address
    00:17:88:19:15:8f
Internal IP Address
    172.28.192.207
Netmask
    255.255.255.0
Gateway
    172.28.192.2
Proxy server address
    none
Proxy server port
    0
```

* Search Sample

```javascript
var hue = require("node-hue-api");

var displayBridges = function(bridge) {
    console.log("Hue Bridges Found: " + JSON.stringify(bridge));
};

// --------------------------
// Using a promise
hue.nupnpSearch().then(displayBridges).done();

// --------------------------
// Using a callback
hue.nupnpSearch(function(err, result) {
    if (err) throw err;
    displayBridges(result);
});
```
result
```
Hue Bridges Found: [{"id":"001788fffe19158f","ipaddress":"172.28.192.191"}]
```

* Hue registing new user

```javascript
var HueApi = require("node-hue-api").HueApi;

var hostname = "172.28.192.191",
    newUserName = null // You can provide your own username value, but it is normally easier to leave it to the Bridge to create it
    userDescription = "device description goes here";

var displayUserResult = function(result) {
    console.log("Created user: " + JSON.stringify(result));
};

var displayError = function(err) {
    console.log(err);
};

var hue = new HueApi();

// --------------------------
// Using a promise
hue.registerUser(hostname, newUserName, userDescription)
    .then(displayUserResult)
    .fail(displayError)
    .done();

// --------------------------
// Using a callback (with default description and auto generated username)
hue.createUser(hostname, null, null, function(err, user) {
    if (err) throw err;
    displayUserResult(user);
});
```

result
```
nifty-5080:hue_demo sci01445$ node hue_register.js
Created user: "3411e73a1d6e01772f87aca6220a5693"
Created user: "80a1244307297623ce3e4f1aa0fe3f"
```

* Light status
Sample code

```javascript
var HueApi = require("node-hue-api").HueApi;

var displayResult = function(result) {
    console.log(JSON.stringify(result, null, 2));
};

var host = "172.28.192.191",
    username = "80a1244307297623ce3e4f1aa0fe3f",
    api;

api = new HueApi(host, username);

// --------------------------
// Using a promise
api.lights()
    .then(displayResult)
    .done();

// --------------------------
// Using a callback
api.lights(function(err, lights) {
    if (err) throw err;
    displayResult(lights);
});
```
result
```
{
  "lights": [
    {
      "id": "1",
      "type": "Extended color light",
      "name": "Hue Lamp 1",
      "modelid": "LCT001",
      "uniqueid": "00:17:88:01:00:d6:84:00-0b",
      "swversion": "5.5.1.9663"
    },
    {
      "id": "2",
      "type": "Extended color light",
      "name": "Testing Hue",
      "modelid": "LCT001",
      "uniqueid": "00:17:88:01:00:e6:02:04-0b",
      "swversion": "66009663"
    }
  ]
}
```

* Interactive with light

```javascript
var hue = require("node-hue-api"),
    HueApi = hue.HueApi,
    lightState = hue.lightState;

var displayResult = function(result) {
    console.log(JSON.stringify(result, null, 2));
};

var host = "",
    username = "",
    api = new HueApi(host, username),
    state;

// Set light state to 'on' with warm white value of 500 and brightness set to 100%
state = lightState.create().on().white(500, 100);

// --------------------------
// Using a promise
api.setLightState(5, state)
    .then(displayResult)
    .done();

// --------------------------
// Using a callback
api.setLightState(5, state, function(err, lights) {
    if (err) throw err;
    displayResult(lights);
});
```
