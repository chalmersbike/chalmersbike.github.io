---
title: How To - Software
---
<!--ts-->
<!--te-->

Table of Contents
-----------------

[**How to share internet with the BeagleBone via USB on Windows**](#how-to-share-internet-with-the-beaglebone-via-usb-on-windows)

[**How to upload code to the BeagleBone from Pycharm**](#how-to-upload-code-to-the-beaglebone-from-pycharm)

[**How to start an ssh session with the BeagleBone**](#how-to-start-an-ssh-session-with-the-beaglebone)

[**How to run code on the BeagleBone**](#how-to-run-code-on-the-beaglebone)

[**How to download results from the BeagleBone**](#how-to-share-internet-with-the-beaglebone-via-usb-on-windows)

-----------------

# How to share internet with the BeagleBone via USB on Windows

1. Plug the micro-USB cable into the BeagleBone

2. Open Network Connections in the control panel. 

    Alternatively enter this into the run window: `ncpa.cpl`

3. Right click on the BeagleBone network adaptor and choose `Properties`. The correct adaptor can be identified by its device name, look for:  `Linux USB Ethernet/RNDIS Gadget` 

<p align="center"><img src="https://github.com/bababash/chalmersbike/blob/master/wiki/howto/BBB_NetworkConfig_2.JPG" width="400"></p>


4. Modify the settings so they match this image and press OK.

<p align="center"><img src="https://github.com/bababash/chalmersbike/blob/master/wiki/howto/BBB_NetworkConfig.JPG" width="400"></p>

5. Close the Properties window

6. Right click on your primary network adaptor and choose `Properties`.

7. Select the `Sharing` tab and modify the settings so they match this image and press OK. If prompted to change the IP of the Beaglebone, press Yes. You may have to repeat step 4 to get it working.

<p align="center"><img src="https://github.com/bababash/chalmersbike/blob/master/wiki/howto/BBB_NetworkConfig_3.JPG" width="400"></p>

8. SSH into the Beaglebone and run the script `usb_internet.sh` located in the root directory of this repo.

# How to upload code to the BeagleBone from Pycharm

some text here

# How to start an ssh session with the BeagleBone

1. Power on the BeagleBone

2. Connect to the BeagleBone. This can be done by:

  a. Plugging in a micro-USB cable to the BeagleBone

  OR
    
  b. Connecting to the BeagleBone WiFi access point. Depending on which BeagleBone you are using you will see one of the following access points:
    * BBB1 SSID = `BeagleBone-63C9`

    * BBB2 SSID = `BeagleBone-132D`

3. Open an SSH client like [Putty](https://www.chiark.greenend.org.uk/~sgtatham/putty/) or [MobaXterm](https://mobaxterm.mobatek.net/) (recommended)

4. Start an ssh session

  a. If you connected using USB connect to `192.168.7.2`

  b. If you connected using WiFi connect to `192.168.8.1`

  Finally enter the details to connect:

  Username: `debian`

  Password: `temppwd`

  Port: `22`

# How to run code on the BeagleBone

1. Start an ssh session with the BeagleBone

2. This guide will assume that the login script executed properly and that your terminal is starting from the 'virtual environment' and you are in the `src` folder. This can be verified by checking that your terminal cursor is preceded by something resembling:

    `(chalmersbike-zI2YTWPT) debian@beaglebone:~/chalmersbike/src$`

    where 

    `(chalmersbike-zI2YTWPT)` is the virtual environment

    `debian@beaglebone` is the user and device name

    `~/chalmersbike/src` is the current folder

  3. Navigate to the folder containing your code:

      `cd foldercontainingcode`

4. Run script

    bash script:
    `./myscript.sh`

    python script:
  `python myscript.py`

####  Example: we have a testing script in the testing/rear_motor folder

    cd testing/rear_motor
    
    python rear_motor.py

# How to download results from the BeagleBone
