# Tasks of the Hardware Designers

The non-limited list of tasks of the hardware designers consists of the:

* development of the **mbed device drivers**;
* integration of the mbed firmware in **mbed OS **;
* development of the **Battery Management System** \(BMS\);
* communication with the software development team using the Agile **SCRUM** Software Development Methodology.

## mbed device drivers

The mbed device drivers should be developed according to the Object Oriented Paradigm \(OOP\), for instance in C++. As a good software developer you should create abstractions for all hardware. For each device that will be interfaced by the mbed, the driver software should be based on at least one **class**. A recommended approach is to divide the software in at least three sections: the **interface** \(e.g. GPSmodule.h\), the **implementation **\(e.g. GPSmodule.cpp\) and **application** \(e.g. GPStest.cpp\) \(see **image below**\).

![OOP Interface/Implementation approach](img/OOP.png)

## Integration of the mbed firmware in mbed OS

ARM mbed OS is an open source embedded operating system designed specifically for the "things" in the Internet of Things \(see **image below**\). It includes all the features you need to develop a connected product based on an ARM Cortex-M microcontroller, including security, connectivity, an RTOS and drivers for sensors and I/O devices.

URL: [https://www.mbed.com/en/development/mbed-os/](https://www.mbed.com/en/development/mbed-os/ "mbed OS")

![mbed OS](img/mbed_os_server.png)

## Battery Management System \(BMS\)

<!-- The battery can for example be a LiPo \(Lithium Polymer\) or a Lithium-Ion battery. The choice is up to you.  
The output voltage of a single cell LiPo battery is +3,7 V DC. This voltage should be transformed to +5 V DC. A DC/DC convertor could be a valuable suggestion. The game box should have to ability to charge the battery. The external connector for charging the battery must be a USB connector. A **Battery Management System** \(see **image below**\) is mandatory to prevent excessive discharge of the battery. Deep discharge of these kind of batteries would cause irreversible damage to the battery.

![Lithium-Ion Battery Management System](/assets/BMS2.jpg) -->

## Communication with the software development team

The team of hardware developers should meet/communicate on a regular basis with the software development team. The use of the iterative and incremental Agile software development methodology of **SCRUM** \(see **image below**\) is mandatory. One of the major contributors to the successful realization of a project is an intense, regular communication between the hardware and the software engineering teams. Detailed agreements on interfaces, connectors, communication protocols, pinout, ... are mandatory and fundamental to guarantee the successful realization of your project within a realistic period of time.

![the Agile SCRUM Methodology of software development](img/SCRUM.jpg)

