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

Simulink model is available [here](https://github.com/chalmersbike/simulink). To run the Simulink model (bike_model.slx), the first section of the initialization code (bike_init.m) should be run first. Simulink version should be at least 2018a.

If you have any question please don't hesitate to ask to the owner of the repository (Umur E., umure@student.chalmers.se).

There are several parameters that need to be change for each bike or simulation in the bike_init.m file:


PARAMETER       | EXPLANATION
---------       | -----------
sim_time           | simulation time [s]
initial_states     | initial states of the bike at t=0 [roll angle in rad, steering angle in rad, roll rate in rad/s]          
input_velocity     | reference speed of the bicycle [m/s]
min_max_velocity   | if variable velocity is used in the simulation, min and max values of the reference velocity profile should be specified here for calculating corresponding dynamics [m/s]
noise              | 1=enable noise on the sensors, 0=disable noise
look_ahead         | 1=enable look-ahead path control, 0=disable (EXPERIMENTAL, NOT FINALIZED!)
fork_dynamics_lqr  | 1=take fork dynamics into consideration for LQR calculation 0=don't consider fork dynamics for LQR
forward_motor_dynamics     | 1=enable forward motor dynamics, 0=disable
steering_motor_limitations | 1=enable limitations (deadband, delay), 0=disable
path_tracking=1;  | 1=path tracking, 0=only self balancing, no path tracking
plant_model       | 1=nonlinear plant, 2=linear plant, 3=linear plant with neglected fork angle (the simplest plant)
roll_acceleration_calculation   | 1=derivate roll rate, 0=use the model to estimate
Ts           | sample time of the controller [sec]
Ts_IMU       | sample time of the IMU [sec]
Dead_Band                        | deadband characteristics for steering motor [Dead Band Limit(+,-), Relay], [rad/sec]
max_steering_motor_acc           | maximum steering motor acceleration [rad/s^2]
min_steering_motor_acc           | minimum steering motor acceleration [rad/s^2]
max_steering_motor_speed   | maximum steering motor velocity [rad/s]
min_steering_motor_speed   | minimum steering motor velocity [rad/s]
delay                      | delay of steering motor [sec]
complementary                    | complementary filter coefficient (0.5<c<1) %0.995
roll_rate_coef                   | coefficient of the low pass filter at the gyro output %0.8
noise_hall                       | variance of hall sensor noise
noise_encoder                    | variance of steering motor encoder noise
noise_gyro                       | variance of gyroscope noise
noise_acc                        | variance of noise of roll angle estimation based on accelerometer                               
max_roll                     | maximum roll angle permitted [rad] // otherwise simulation stops
max_handlebar                | maximum handlebar angle [rad] before the saturation
min_roll                     | minimum roll angle permitted [rad] // otherwise simulation stops
min_handlebar                | minumum handlebar angle [rad] before the saturation
h             | height of the center of mass (see the paper for more details)
b             | length between the wheel centers (see the paper for more details)
a             | horizontal distance from rear wheel to the center of the mass (see the paper for more details)
c             | length between front wheel contact point and the extention of the fork axis [m]
lambda        | angle of the fork axis [rad]
IMU_height    | IMU height [m]    
Q               | cost of the states for the LQR controller
R               | cost of the inputs for the LQR controller
plots          | Set to 1 to see the plots [eigenvalue plot, path plot]
radius          | radius of the path if the path is circle [m]
x_ini_diff      | initial off-set in x direction for the reference path
y_ini_diff      | initial off-set in y direction for the reference path
path            | path to be followed, out of 9 pre-determined paths

The second section of the initialization code is to generate performance plots after simulation and the third section is to generate plots for comparing the real test results and the simulation results.

