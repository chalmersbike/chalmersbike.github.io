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

## How to modify
