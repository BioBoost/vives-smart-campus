# Hardware requirements

## Game Box

The "game box" \(one per team\) is a plastic box and will be provided \(see the image below \). The game box will contain the battery, the battery management system, an LCD display, the embedded system, ..., so that the competing teams should have an autonomy of several hours.

<!-- ![Example of the game box](/assets/SVL_003_2021.jpg) -->

Consider the following overview of the hardware components:

* a battery \(Lithium Ion Polymer - LIPO\);
* a battery management system to charge the battery and keep track if its minimal voltage level;
* an FRDM-K64F **mbed **based embedded system \(URL: [https://developer.mbed.org/platforms/FRDM-K64F/](https://developer.mbed.org/platforms/FRDM-K64F/ "FRDM-K64F mbed") - see **Figure 3/4**\) to host the firmware;
* a Real Time Clock \(RTC\) to provide day/time timestamps;
* an LCD display \(4 x 20 characters\) to visualize messages, tasks, challenges, the user interface, ...;
* a keyboard for user input;
* a key lock for challenges;
* five LED's for status indications;
* and two pushbuttons

![FRDM-K64F mbed](img/FRDM_K64F_large.png)

![FRDM-K64F mbed Block Diagram](img/xfrdm-k64f_block-diagram_jpg_pagespeed_ic_n9RhjOFW_9.jpg)

## Game Box hardware extensions

The basic hardware of the game box must be extended with the following hardware components:

* a **GPS** module
* a **LoRaWAN** transceiver \(URL: [https://www.lora-alliance.org/For-Developers/LoRaWANDevelopers](https://www.lora-alliance.org/For-Developers/LoRaWANDevelopers "LoRaWAN") - see **see image below**\)

**LoRaWAN** is a Low Power Wide Area Network with features that support low-cost, mobile, and secure bi-directional communication for Internet of Things \(IoT\), machine-to-machine \(M2M\), smart cities, and industrial applications. LoRaWAN is optimized for low power consumption and is designed to support large networks with millions of devices. Innovative features of LoRaWAN include support for redundant operations, geolocation, low-cost, and low-power devices can even run on energy harvesting technologies enabling the mobility and ease of use of Internet of Things.

![LoRaWAN Network Architecture](img/LoRaWAN_network_architecture.jpg)

The LoRaWAN communication channel can be used to implement the real-time monitoring of the game state by the game master. Since it is a bi-directional channel, it can also be used by the game master to change settings or inject challenges in the team's game-boxes.
