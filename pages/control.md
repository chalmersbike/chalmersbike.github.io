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

This wiki page is about the simulation of Chalmers Autonomous Bicycle Project.

# THEORETICAL BACKGROUND

Please see the  following articles for the details of control scheme used in this bike simulations:

[Modelling and control of an Autonomous Bicycle](../docs/Modelling%20and%20control%20of%20an%20Autonomous%20Bicycle.pdf)

[Bicycle Dynamics and Control](https://lup.lub.lu.se/search/ws/files/4692388/625565.pdf)

# FILES IN THE REPOSITORY

Simulink model is available [here](https://github.com/chalmersbike/simulink). There are 2 files to run:

FILE NAME       | EXPLANATION
---------       | -----------
bike_init.m     | Matlab m file to initialize the simulation variables and take the graphical results.
bike_model.slx  | Simulink file for the simulation. (Matlab 2018a is required.)

Please put all files to the same directory and be sure that your Matlab version is at least Matlab 2018a.

# A SHORT INTRODUCTION TO INITIALIZATION CODE

In bike_init.m file there are 4 sections of the code:

SECTION    | EXPLANATION
---------  | -----------
1          | Initializes the simulation variables and settings. It should be run before the simulation. It also plots the path to be followed and eigenvalues of the system for stability analysis. Plots can be turned off and on depending on the choice.
2          | Runs the Simulink simulation (by calling bike_model.slx file).
3          | It should be run after the simulation. It gives "reference path vs followed path" and "bike path errors" graphs. Plots can be turned off and on depending on the choice.
4          | It is for generating plots where real test and simulation results are presented together. Do not use it if you don't want to compare real test and simulation results. It requires the real test files in csv format. In default, this section is turned off, so the code file skip that part.

One can run bike_init.m file all together at once; in this case, simulation variables and settings will be created, simulation will run automatically, and then resulting plots will be automatically created. Another option is to run the first section of the bike_init.m, and then to run bike_model.m file manually. By this, one can locate scopes to certain signals to have particular results. Then third section of the bike_init.m can be run after simulation for further plots for the results.

# A SHORT INTRODUCTION TO SIMULATION

Simulation file bike_model.slx has several important blocks that represent:

BLOCK                     | TYPE               | EXPLANATION
---------                 | -----------        | -----------
physical bicycle          | bike               | without sensor or actuators
forward velocity motor    | actuator           | actuates the bike to front direction
steering motor            | actuator           | steers the steering bar
hall effect sensor        | sensor             | measures the forward speed
inertial measurement unit | sensor             | measures the roll angle and roll rate
steering encoder          | sensor             | measures steering angle
balance controller        | controller         | controls the bike so that it balances itself, calculates the steering input (steering rate)
path controller           | controller         | controls the bike so that it follows a predetermined trajectory, calculates the reference steering angle to follow the path
global coordinate calculator| calculation      | calculates the global coordinates of the bicycle

# A MORE DETAILED EXPLANATION OF THE SIMULATION

This simulation is intended to simulate the dynamics of the real bike. So, one needs to include every kind of detail that esixt in the real life, like sensor noise, signal delay, dead-band, hysterisis, maximum acceleration limitations, etc.

In the following table, real life limitations and details taken into consideration for each sub-system of the bicycle is presented:

BLOCK                     | DETAILS
---------                 | ----------- 
physical bicycle          | several different plant models are possible to simulate (linear, nonlinear, etc)
forward velocity motor    | dynamics of the forward velocity motor (designed as a transfer function)
steering motor            | max/min speed, max/min acceleration, dead-band, hysteresis, delay, max/min steering angle permitted
hall effect sensor        | noise on the measurements, minimum possible measurement
inertial measurement unit | noise on the accelerometer and gyroscope measurements, several different filters to estimate the roll angle, different sampling time then the rest of the components, dimensions of the point where IMU is placed can be specified
steering encoder          | noise of the measurements
balance controller        | different plant models are available to calculate the LQR control law
path controller           | an experimental look-forward path planning alghoritm is available (NOT FINALIZED!)


If you have any question please don't hesitate to ask to the owner of the repository (Umur E., umure@student.chalmers.se).

There are several parameters that need to be change for each bike or simulation in the bike_init.m file:


PARAMETER          | EXPLANATION
---------          | -----------
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



