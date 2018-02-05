# Hardware Requirements

Multiple hardware systems must be build. 
1. Occupation detector
2. Temperature and humidity monitoring
3. Smart signs

Designing and developing these systems must be done in an incremental process. Start by using development boards, breadboards and sensors. This enables to do small experiments and start writing the firmware. Parallel a custom board can be developed. This process makes sure that hardware and firmware can be developed without depending on each other.

Any hardware can be used. The only requirement is that it is mbed compatible: [developer.mbed.org/platforms/](https://developer.mbed.org/platforms/).

## LoRaWAN Transceiver

All designs must make use of LoRaWAN. Multiple transceivers are available on the market. You can choose any of these radio's:
* HopeRF RFM-95
* Microchip RN2483
* Murata CMWX1ZZABZ
* ...

## Battery Powered

All designs must be battery powered. Special attention is needed to make sure the hardware consumes the least possible amount of power. The hardware must be able to run on 3 AAA batteries for at least 1 year. 

An AAA battery has a typical capacity of around 1000mAh. 1 year consists out of 8760 hours. This means that the hardware must consume less then 1000mAh / 8760h = 0.114mA. Keeping in mind the self discharge of a battery, lets set the limit of average power consumption at 0.100mA or 100µA. Thus building an Ultra Low Power circuit.

The design must result in a circuit that consumes as less as possible. If an lifetime of more than 1 year can be achieved, than this will be rewarded.

## Occupation Detector

The heart of the occupation detector is a digital PIR sensor: Panasonic AMN31111j. This PIR sensor is really easy to use. The output pin will toggle whenever the sensor detects movement.

The detector should be enclosed in a plastic case. At the bottom an magnet should be placed so that the sensor can stick to any iron surface (casings, cabinets, ceiling,...). These enclosures can be found at [be.farnell.com](http://be.farnell.com). Magnets can be selected at [www.supermagnete.be](http://www.supermagnete.be).

The detector should accumulate the movement detections over a fixed or variable amount of time and send a summary to the server. For example detected 12 movements in the last minute, or detected only 1 movement in the last 3 hours.

The detector should also be able to send a periodic heartbeat to the server, letting it know that it is still functioning. 

The detector must also let the server know what the state of the battery is. This could be on a daily basis or an other interval.

## Temperature and Humidity Monitor

The temperature and humidity monitor should build further on the existing occupation detector. Expand the existing design to add the new functionality. Keep in mind that the power consumption may not exceed the existing limit of 100µA average. The same enclosure must be compatible with these new features.

## Smart Signs

To build the smart signs, an power efficient technology must be used. Epaper is an excellent option for this kind of cases. The same power restrictions apply for the smart signs. The battery must last at least for 1 year without replacing them. 

The smart signs must have a notion of the current time. Therefore an Real Time Clock or RTC must be available to the system.

The smart signs must support at least two use cases.
* Classroom labels
* Signposts

### Classroom labels

A summary of the schedule of the current day must be visible on the display. The current occupation of the room must be highlighted. The schedule consists out of the following properties:

* Room number
* Current date
* Course name
* Teachers involved to the course (could be multiple)
* Start hour
* End hour

### Signposts

Signposts will be placed in the hallway or building entrance. They will inform visitors and students of special events. For example if an event or workshop is held on a particular day, it must show the following information:

* Name of the event
* Start hour
* End hour
* Room number
* Arrow pointing to the room

When no events are planned for that day, information about upcoming events can be displayed, or a simple welcome message.
