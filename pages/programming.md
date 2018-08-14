---
title: Programming
---
[Home](http://chalmersbike.github.io)

<!--ts-->
   * [Motor Control - MSP430](#motor-control---msp430)
      * [How it works](#how-it-works)
      * [Important information](#important-information)
      * [How to modify](#how-to-modify)
   * [IMU Data -Arduino](#imu-data--arduino)
      * [How it works](#how-it-works-1)
      * [Important information](#important-information-1)
      * [How to modify](#how-to-modify-1)
   * [Bike Computer - Beaglebone Black](#bike-computer---beaglebone-black)
      * [How it works](#how-it-works-2)
      * [Important information](#important-information-2)
      * [How to modify](#how-to-modify-2)

<!-- Added by: Boaz Ash, at: 2018-08-10T16:47+02:00 -->

<!--te-->

# Motor Control - MSP430

A TI MSP430F5529 Microcontroller is used to send the PWM signals to the motor controllers used on the bike.

## How it works

The BeagleBone connects to the MSP430 using serial communication. The Beaglebone sends a string which indicates which motor should have its input changed and what the input is.

## Important information

The MSP430 generates three PWM outputs on `P1.2`, `P1.3`, `P1.4` using Timer_A configured for UP mode.
The PWM period has been set at 20ms.


Each actuator has a unique code to identify it when the Beaglebone sends a serial command.

```
//  The input code for the Jaguar Steering Motor is #
//  The input code for the Jaguar Brake Actuator is $
//  The input code for the Turnigy Shimano Motor is %
```


The actuator pulse widths have been defined below:

```
//  JAGUAR
//  TA0CCR = 710; // corresponds to 0.67ms (Jaguar full reverse)
//  TA0CCR = 1580; // corresponds to 1.5ms (Jaguar neutral)
//  TA0CCR = 2450; // corresponds to 2.33ms (Jaguar full forward)
//
//  TURNIGY
//  TA0CCR = 1050; // corresponds to 1.0ms (turnigy neutral)
//  TA0CCR = 2100; // corresponds to 2.0ms (turnigy full forward)
//
//  MAXON
//  TA0CCR = 1050; // corresponds to 1.0ms (maxon full reverse)
//  TA0CCR = 1580; // corresponds to 1.5ms (maxon neutral)
//  TA0CCR = 2100; // corresponds to 2.0ms (maxon full forward)
```

## How to modify

You will need to use Texas Instruments [Code Composer Studio](http://www.ti.com/tool/CCSTUDIO). 



# IMU Data -Arduino

## How it works

## Important information

## How to modify

# Bike Computer - Beaglebone Black

## How it works

## Important information

### Beaglebone info:

* Default USB IP: `192.168.7.1`

* Default WiFi IP: `192.168.8.1`

* Default Wifi Password: `BeagleBone`

* BBB1 SSID = `BeagleBone-63C9`

* BBB2 SSID = `BeagleBone-132D`

* Login Username: `debian`

* Login Password: `temppwd`

### Beaglebone First Run:
* Manually setup internet access:
Connect the beaglebone via USB. 

  On Windows set IP of BBB to `192.168.7.2` and gateway+DNS to `192.168.7.2` also make sure you are sharing your ethernet connection.
  Follow the usb_internet.sh script:
  
  `sudo /sbin/route add default gw 192.168.7.1`
  
  `echo 'nameserver 192.168.7.1' | sudo tee --append /etc/resolv.conf`

* Update, upgrade OS and Kernel

  `sudo apt-get update`

  `sudo apt-get upgrade`

  `sudo reboot`

  `cd /opt/scripts/tools`

  `sudo ./update_kernel.sh`

  `sudo reboot`


### Internet Access
To connect to the internet, attach the usb cable and run `usb_internet.sh` in the root folder

## Using the repo

Clone the repo

`git clone https://github.com/bababash/chalmersbike.git`
`cd chalmersbike`

### Setup virtual environment and install required packages

`sudo apt-get install build-essential libi2c-dev i2c-tools python-dev libffi-dev`

`sudo pip install pipenv`

`pipenv install --two`


### Pin Configurations

These are the pins to use for the external connections. Please refer to [Beaglebone Cape Pins](http://beagleboard.org/static/images/cape-headers.png) for a diagram

* Shimano Steps: P8.10
* SDA (IMU): P9.20
* SCL (IMU): P9.19
* UART TX (MSP430 RX P3.4): P9.24
* UART RX (MSP430 TX P3.3): P9.26
* Hall Sensor: P9.12
* Encoder CH.A: P8.12
* Encoder CH.B: P8.11
* Encoder CH.I: P8.16
* PWM Output (MSP430 P1.3): Jaguar Motor Controller

### Initial setup
To make sure all these pins are assigned to their proper functions, run `config_pin.sh`

### Config stuff
The beaglebone can be set to autorun the init codes on login. The file that must be changed is `/home/debian/.bashrc`
The lines that must be added are:

`cd ~/chalmersbike`

`./config-pin.sh`

`pipenv shell`

`cd src`


## How to modify
