---
title: Control
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

Please see the article [Modelling and control of an Autonomous Bicycle](../docs/Modelling%20and%20control%20of%20an%20Autonomous%20Bicycle.pdf) for an in depth discussion of the bike model and the development of our controller.

Simulink model is available [here](https://github.com/chalmersbike/simulink). To run the Simulink model (bike_model.slx), initialization code (bike_init.m) should be run first.

There are several parameters that need to be change for each bike or simulation in the bike_init.m file:

input_velocity  : constant forward velocity input
Dead_Band       : steering motor dead band characteristics
discrete        : 1 if the simulation is discrete, 0 if the simulation is continuous
Ts              : sample time of the simulation
delay           : delay in the steering motor
plots           : plots for eigenvalues of the system ( A - B * K) and plot for the path
radius          : radius of the path if the path is circle 
x_ini_diff      : initial off-set in x direction for the reference path
y_ini_diff      : initial off-set in y direction for the reference path
path            : path to be followed, out of 9 pre-determined paths

MAX_ROLL            : maximum roll angle to stop the simulation
MAX_HANDLEBAR_ANGLE : maximum handlebar angle (saturates beyond this limit)
MIN_ROLL            : minimum roll angle to stop the simulation
MIN_HANDLEBAR_ANGLE : minimum handlebar angle (saturates beyond this limit)

h : height of the center of mass (see the paper for more details)
b : length between the wheel centers (see the paper for more details)
a : horizontal distance from rear wheel to the center of the mass (see the paper for more details)


Q               : cost of the states for the LQR controller
R               : cost of the inputs for the LQR controller
Qn, Rn, H, G, N : Kalman filter parameters 

