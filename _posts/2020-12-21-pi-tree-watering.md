---
layout: post
title: Raspberry Pi Tree Watering System
published: true
author: ypanshin
comments: true
tags:
    - Raspberry PI
    - Ionic
    - React
categories:
    - technology
permalink: /technology/pi-tree-watering.html
image:
    feature: /assets/posts/2020-12-21-pi-tree-watering/diagram.png
---
For a long time, I planned to build a Christmas tree watering system as I always forget to water the Christmas tree on time.
<!--more-->

This year I have finally done this. The most complicated part was to find the moisture sensor, as that one that I bought was killed by the rust in several days. The rust made the sensor's deep sticks broke the connection, and the sensor was showed it is dry, which costs me a pound around the tree base. 
The next attempt was with a regular cooper wire as the moisture sensor deep stick.
Some rust covered the cooper wires as well, but at least it continued to work.

## Devices
- [Raspberry PI any model](https://amzn.to/3nE8tsk)
- [Relay JQC-3FF-S-Z](https://amzn.to/38jBsez)
- [Moisture Sensor](https://amzn.to/3h5OksS) Do not recommend this one, as it only holds for one week after it broke because of rust. I already ordered another sensor type for the test. However, I used the sensor's processor.
- [Water Pump](https://amzn.to/2WwcDGI)

## Storage [JsonBox](https://jsonbox.io/)
The system uses JsonBox to store the logs.
- navigate to the link and get the box id from the link on hte home page
## System Setup
![Diagram](/assets/posts/2020-12-21-pi-tree-watering/diagram.png)
### Relay
Connect the relay to the Raspberry PI:
- VCC --> Pin 2 (5V)
- GND --> Pin 20 (Ground)
- IN  --> Pin 22 (GPIO 25)

### Moisture Sensor
Connect the moisture sensor to Raspberry PI:
- VCC --> Pin 4 (5V)
- GND --> Pin 6 (Ground)
- DO  --> Pin 3 (GPIO 2)
The original sensor did not hold for me for more than a week. Rust destroyed the sensor. I replaced this sensor with two regular copper wires used for the house's electricity, and it worked much better. 
### Water Pump
Connect the water pump to the relay:
- plus --> COM
- minus --> DC Power Supply minus
- Relay ON --> DC Power Supply plus

### Application Installation on Raspberry PI
- `$ git clone https://github.com/ypanshin/pi-tree-watering.git` - clone the repository
- `$ cd pi-tree-watering` - navigate to the project folder
- `$ nano package.json` - update `config` section of `package.json`
```
"config": {
    "sensorPin": 3, // the pin that moisture sensor connected to.
    "relayGpio": 25, // the GPIO that the relay connected to
    "onInterval": 1000, // the interval in ms to check the moisture sensor when the relay is on (the pump is working).
    "offInterval": 60000, // the interval in ms to check the moisture sensor when the relay is off (the pump is not working).
    "pumpFlow": 1.5, // the pump flow in litters per minute
    "maxLogItems": 1000, // the maximum items in the log
    "binId": "box_6f937824ca2f42a8a471" // the box id
  },
```
- `$ npm i && npm run build && npm start` - install, build and run the application

### Run the application On Raspberry Pi At Startup
Running the application on boot:
```
sudo nano /etc/rc.local
```
On the line before `exit 0` write the following script, replacing `{path to application}` with the directory of your application
```
su pi -c 'sudo npm start --prefix /home/pi/{path to application} < /dev/null &' 
```
Write out the lines to save them (CTRL-X) and then `$ sudo reboot` to restart your RPi

## [Dashboard](https://pi-tree-watering.tech.panshin.me)
The dashboard is an Ionic / React application that displays statistics and logs from the JsonBox log file.
Please use the JsonBox Id configured in your Raspberry Pi Application, or for the demo, you can use mine: `box_6f937824ca2f42a8a471`