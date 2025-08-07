Hello World

### Summary

The 2025 SAHA SAO consists of two major components: 
- [Ublox BMD 300](https://www.u-blox.com/en/product/bmd-3035-series-open-cpu)
- [TI LP55231 LED Driver](https://www.ti.com/product/LP55231)

The BMD 300 contains an [nRF52832](https://www.nordicsemi.com/Products/nRF52832) which handles LED Driver setup and the SAO proximity function.
By using an LED driver the animation of the 5 LEDs does not depend on the processor to keep the appearance smooth.
The LED driver operates completely independently of the processor with the sole exception of the proximity indicator which has its state updated periodically based on BLE scans.

The average power consumption of the SAO is 6.5 mA, giving around 30 hours of run time with a 200 mAh CR2032 coin cell battery.

INSERT PICTURES OF THE SAO HERE

The [github repo](https://github.com/ChipWizards/SAHA-SAO) contains:
- Schematics showing how the SAO is wired
- The TI assembler to build programs for the LP55231 LED Driver
- Source code for the SAO firmware

### Proximity Feature

The proximity feature works with each SAO simultaneously broadcasting and receiving beacons.
The PWM duty cycle of D1 (the soldering iron) is determined by the RSSI of received beacons.
If there are multiple beaconing SAOs being received D1 will appear to switch between multiple brightness settings, this is an intentional choice to help represent multiple beacons being received.

### Headers

There is an SWD header for flashing and debugging custom firmware that follows the SWD standard.

INSERT DIAGRAM OF PINOUT

The SAO header in the center follows the SAO standard with the addition of TX and RX in case there are users who wish to use a carrier badge to communicate with the SAO via UART.

INSERT DIAGRAM OF PINOUT

### Debugging

Users wanting to flash custom firmware will need a debugger to do so.
nRF prefers the JLink line of debuggers, these are going to be the most tightly integrated debuggers for this set up.
The Segger JLink Edu Mini will be the most effective.

The best places to buy these would be here:
- [Direct from Segger](https://shop-us.segger.com/product/j-link-edu-mini-8-08-91/)
- [Mouser](https://www.mouser.com/ProductDetail/Segger-Microcontroller/8.08.91?qs=gt1LBUVyoHmQKgW9PvZ%2FwQ%3D%3D)

It may be possible to use other SWD capable debuggers to program the SAO using OpenOCD.
These other debuggers won't be integrated into nRF's IDE (vscode) correctly but will work outside of it.

### Getting started with custom firmware

The [nRF academy](https://academy.nordicsemi.com/courses/nrf-connect-sdk-fundamentals/lessons/lesson-1-nrf-connect-sdk-introduction/) has the best documentation for setting up their SDK.
It's worth it to walk through lesson 1 to set up the SDK and learn how to build examples.
Beyond Lesson 1 is a good primer for developing firmware for nRF devices but the following lessons are not required reading for tinkering with the SAO.

### HOW DOES THE LED DRIVER WORK? TODO