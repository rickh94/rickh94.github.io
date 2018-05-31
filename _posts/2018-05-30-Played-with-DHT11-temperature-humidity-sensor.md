---
title: Played with DHT11 temperature/humidity sensor
layout: post
category: automation
tags: arduino dht11 sensors automation esp8266
---

I worked with the dht11 temperature/humidity sensor. The libraries are quite
nice and worked well once I realized that I had missed the ground pin on the
breadboard by one spot. Same mistake twice. If there is no valid signal,
always check ground first, it would be great not to mess that up again.

Once it was working I did discover that there is significant latency (several
reads) before the sensor reacts, so code based on it should run slowly.

I also found an [arduino sketch](https://gist.github.com/balloob/1176b6d87c2816bd07919ce6e29a19e9#file-mqtt_esp8266_temperature_humidity-ino) specifically for an esp8266 mqtt temp/humidity
sensor so that's convenient.
