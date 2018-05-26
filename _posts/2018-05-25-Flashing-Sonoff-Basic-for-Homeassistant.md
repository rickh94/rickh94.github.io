---
title: Flashing Sonoff Basic for Homeassistant
layout: post
category: automation
tags: sonoff homeassistant automation flashing platformio serial ftdi wiring mqtt wifi
---

I flashed my first sonoff basic chip based on the esp8266 mcu. The
[firmware](https://github.com/arendst/Sonoff-Tasmota) is pretty nice and
intuitive, though there were a few issues.

## Flashing

PlatformIO is super nice, but a little picky. My first issue was with the
serial port for flashing. It is set in the plaformio.ini file and needs to use
and ABSOLUTE PATH to the terminal (i.e. /dev/ttyUSB0).

I had a weird issue flashing the first time, but redoing it fixed it. It
showed up in homeassistant and I was able to configure a few things using the
web portal.

Sometimes it gets weird errors when going directly to upload, but manually
building and then uploading usually takes care of that.

## Hardware

Wiring is not too bad for flashing, my custom ftdi cable is nice. Remember RX
<-> TX. The wiring of the ac cables is a PAIN, they kept coming apart. The
strain relief from the plastic chassis piece is absolutely required, the wires
will pull out of the terminals without it.

Also the ridged wire on an ac plug is neutral, the smooth is live.

## Configuration

# Basic

The initial configuration was a little annoying, but I more or less got it.

1. It is best to define USE_CONFIG_OVERRIDE and leave the default file alone.
1. It is essential to define CFG_HOLDER to a new value (the date works) or it
   will not rebuild the configuration. I think this is the problem I had the
first time
1. undef then define any variables to change

# MQTT

I'm using sub_prefix switches to control the various smart switches and just
naming them SONOFFX. Since homeassistant is handling things, I can give them
descriptive names there.

I generated a password for each switch and gave them descriptive usernames.
These can be added to the /etc/mosquitto/passwd file with `sudo
mosquitto_passwd -b /etc/mosquitto/passwd USERNAME PASSWORD`. It is important
not to use -c or -U on existing files because this will overwrite the file or
hash the already hashed passwords, basically meaning those users have to be
configured again from scratch.

# Homeassistant

I've included switches.yaml for switches. The basics of the config are:

{% highlight yaml %}
- platform: mqtt
  name:
  state_topic: "sonoff/SONOFFX/RESULT"
  value_template:{% raw %} '{{ value_json["POWER"] }}' {% endraw %}# this line is required
  command_topic: "switches/SONOFFX/POWER"
  availability_topic: "tele/SONOFFX/LWT"
  qos: 1
  payload_on: "ON"
  payload_off: "OFF"
  payload_available: "Online"
  payload_not_abailable: "Offline"
  retain: true
{% endhighlight %}

and then restart homeassistant and it will show up.
