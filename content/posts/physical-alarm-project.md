---
title: "Physical Alarm Project"
date: 2020-06-16T20:16:14+02:00
mermaid: true
tags:
 - DIY
 - IoT
---

# An old idea resurrected

In the end of 2019 when me and my team discussed how we at Homegate are going to tackle SRE topics I had this idea of having a physical
alarm going off when an alarm from DataDog's monitor snaps. We're using a Rapsberry Pi 4 to display our dashboard so a logical way would 
be to drive one of those alarms using one of its GPIOs.

But I thought it's a little to boring. I also remembered that I have a few [PADI IoT Stamps](https://store.pine64.org/padi-iot-stamp/) and
I thought this is a perfect use case for them.

It's based on Realtek RTL8710AF SoC, which is supported in Arduino thanks to [RtlDuino](https://github.com/pvvx/RtlDuino) so I could use 
[Blynk](https://blynk.io/) with its [libary](https://github.com/blynkkk/blynk-library) to control it via Internets. This way I could wire
it via WebHooks in either DataDog or [IFTTT](https://ifttt.com/maker_webhooksa).

So I went to AliExpress and order [these](https://www.aliexpress.com/item/32296386340.html?spm=a2g0s.9042311.0.0.20064c4dAM3bZ4) amazing 
alarm strobes

[!Alarm Strobe](./images/alarm.jpg)

along with 12V AC/DC adapters and DC-DC converters (PADI IoT Stamp runs of 3.3V).

## General architecture

{{<mermaid>}}
graph LR;
A[DataDog]-->|Webhook call| B(Blynk.io);
B-->C[PADI];
C-->D(Alarm);
{{</mermaid>}}
