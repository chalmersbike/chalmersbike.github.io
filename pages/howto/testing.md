---
title: How To - Testing
---

Menu:

* [Project Overview](https://chalmersbike.github.io/pages/overview.html)

* [Electronic Design](https://chalmersbike.github.io/pages/electronics.html)

* [Programming](https://chalmersbike.github.io/pages/programming.html)

* [Mechanical Design](https://chalmersbike.github.io/pages/mechanical.html)

* [Control](https://chalmersbike.github.io/pages/control.html)

* [How-To Guides](https://chalmersbike.github.io/pages/howto/)

* [Bugs and Troubleshooting](https://chalmersbike.github.io/pages/bugs.html)

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
