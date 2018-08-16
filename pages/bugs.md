---
title: Bugs and Troubleshooting
---
<!--ts-->
   * [IMU waiting for calibration](#imu-waiting-for-calibration)
   * [Manually entering virtualenv](#manually-entering-virtualenv)
   * [Replacing fuses](#replacing-fuses)
   * [Checking and updating date/time on BBB](#checking-and-updating-datetime-on-bbb)

<!-- Added by: Boaz Ash, at: 2018-08-10T16:46+02:00 -->

<!--te-->

# IMU waiting for calibration

Sometimes when the Bike class is intialised in Python, the IMU doesn't begin its calibration process.

If you see the text: `Waiting for calibration` appearing endlessly, you have encountered this bug.

The solution is to reset the Arduino by pressing the reset button. After you press the button, the IMU will calbirate (so don't touch the bike or the box after you push the button.

You will notice that within several seconds the python code continues.

# Manually entering virtualenv

If for some reason the login script which starts the virtual environment doesn't run, here is how to manually enter the virtual environment which contains all of the dependencies for the code.

Using pipenv (the easiest option):

`cd ~/chalmersbike`

`pipenv shell`

If this does not work, this is the procedure to manually enter the virtual environment:

`source ~/.virtualenvs/chalmersbike-zI2YTWPT/bin/activate`

# Replacing fuses

There are four fused terminal blocks inside the enclosure. In order to replace them, open the plastic hinged door and insert the new fuse.

1. Low power electronics: `3A`

2. STEER: `10A`

3. DRIVE: `10A`

4. BRAKE: `10A`

# Checking and updating date/time on BBB

When you run a test, you want the logfile to have the correct date and time. When the Beaglebone is switched off, it does not keep track of the time so you will need to either:

1. Connect the Beaglebone to the internet

2. Manually set the date and time

You can check the current time by typing: 

`date`

## How to manually set the date and time

To set the day: `date --set 1998-11-02` (In the format YYYY-MM-DD)
To set the time: `date --set 21:08:00` (In the format HHMMSS using 24 hour clock)
