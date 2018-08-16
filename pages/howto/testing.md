---
title: How To - Testing
---
<!--ts-->
<!--te-->

# General advice

Before running a test, make sure that:

* The steering wheel is straight and that the bike is vertically upright and stationary. The IMU will calibrate when you start the code and it should not be disturbed during this time.

* [The date and time are correct](https://chalmersbike.github.io/pages/bugs.html#checking-and-updating-datetime-on-bbb)


# How to Easy Start

There is a script to easily run the bike with the controller active.

`cd ~/chalmersbike/src`

`python easystart.py`

# How to stop a test

The controller has four conditions for ending a test.

1. Emergency Stop

2. Keyboard break (press `Control + C`)

3. Exceeded Test Time

4. Exceeded roll limit
