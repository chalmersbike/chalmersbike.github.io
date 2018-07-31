---
title: Electronics
---

# Overview:

The bike has several electronics components that will be detailed below.


![Electrical Overview](https://github.com/bababash/chalmersbike/blob/master/wiki/Electrical%20Overview.svg)

# Components
* **BeagleBone Black Wireless** - this is the computer that implements the controller, communicates with all the sensors and  controls the actuators

* **Launchpad MSP430** (EXP430F5529LP) - this is a real-time microcontroller that is responsible for generating the PWM pulses for motor controller. It is connected to the BeagleBone via serial which means that only one character can be sent at a time. The benefit of a real-time microcontroller is its speed and reliability. If instead the BeagleBone was generating the PWM signals and it had to service an interrupt, the signal may be affected which could result in loss of motor control

* **Hall Effect Sensor** (Honeywell 103SR13A-1) - this sensor is used to measure the forward velocity of the bike. A set of five neodymium magnets were mounted on the rear wheel and the Hall Effect sensor generates a pulse when they travel past it

* **IMU** (Inertial Measurement Unit, MPU6050 mounted on a PCB designed by Niclas Hillborg) - this is a 9 axis sensor that is used to obtain the roll angle and rate of rotation of the bike

* **Encoder** (HEDS5540) - this is the encoder for the steering motor. It has 3 channels and can determine the position of the motor shaft with very high precision

* **Jaguar Motor Controller** (MDLBDC24) - This controller converts the PWM signals from the Launchpad into voltage across the motor terminals. It allows for forward and reverse rotation.

* **Arduino Uno** - This is used to read the values from the IMU and to apply the complementary filter. It replaced the old configuration where the IMU was directly connected to the Beaglebone using the I2C protocol, this was too slow for real-time operation. The current setup has been validated for our purposes.

* **6S Lipo Battery** - Used to power the system.

## Schematic

To interface all of these sensors and provide the correct voltages, several other components were required. The connections and components are detailed in the schematic below.

![Schematic](https://github.com/bababash/chalmersbike/blob/master/wiki/BIKE_SCHEMATIC.sch.svg)


The major components are:
* **Traco Power DC/DC Converter** (TEN 8-2411WI) - This takes our battery voltage as an input and outputs 5V DC.

* **3.3V Linear Regulator** (LM317_T03) - Provides 3.3V to power our sensors

# Safety Relay

An Omron G9SE-201 Safety Relay has been included in the enclosure to shutdown all motor power in case of runaway conditions. This is a category 4 emergency stop setup.

There are several components required:
* S1: E-STOP button
* S2: Reset Switch
* KM1, KM2: **Schneider LC1D12BL 24VDC, 12A contactors**


![Safety Relay Diagram](https://github.com/bababash/chalmersbike/blob/master/wiki/SafetyRelay.svg)

The electrical setup was completed according to the [Omron manual for the safety relay: Section 5, Page 2](https://www.omron.com.au/data_pdf/mnu/g9se-201_-401_-221-t__inst-4022078-4c.pdf?id=3419).

# Future Work

* Add an inline fuse between the battery and the first connector.

The electrical setup for the bike is very messy and it’s begging for a redesign that is more accessible, robust and neater. A PCB for this project would make it much more professional. Current electrical upgrades include:

* An external power supply input be nice so that we can test the electronics without having the bike around or constantly recharging the batteries

* A voltage and current monitor for the batteries to prevent discharging them beyond their safe limits. This would also allow us to monitor power consumption and identify areas for future improvement

* The cables all terminate with screw terminals which makes rewiring very annoying. It is also very hard to identify signal cables. The new circuit should have better connectors

* The sensors are housed in broken out modules that could probably purchased as surface mount modules and get mounted directly to the PCB

* There are no LEDs to indicate functionality of the circuit

* There is no reverse polarity or over-voltage protection

* The BeagleBone cannot have any voltage applied to its pins before it is properly on. We need to design a buffer wait until the BeagleBone is ready

* The voltage regulators should be swapped to DIN rail mounted modules. This eliminates one custom designed protoboard inside the enclosure. We need 5V and 3.3V rails.
