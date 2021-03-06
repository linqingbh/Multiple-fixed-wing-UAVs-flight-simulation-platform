# Multiple fixed-wing UAVs flight simulation platform

## [传送门->中文的说明](READMEch.md)

## 1. Introduction

A multiple fixed-wing UAVs flight simulation platform built by matlab and simulink.

The example given here has 5 UAVs, but of course you can expand it to 10, 20 or even more if you are willing to take the time.

Input: The path of all uavs 

Output: 13 state quantities per drone per moment
    
    pe1            % inertial East position
    pd1            % inertial Down position
    u1             % body frame velocities
    v1              
    w1            
    phi1           % roll angle         
    theta1         % pitch angle     
    psi1           % yaw angle     
    p1             % roll rate
    q1             % pitch rate     
    r1             % yaw rate    
    t1             % time

![avatar](picture/1.gif)

---

## 2. The original intention of platform building

Recently, there is a need to extend the algorithm of cooperative control to fixed-wing UAVs, but the cooperative control algorithm generally considers first-order and second-order integrators or a single vehicle model. Even if a fixed-wing model is considered, it is only a simple fixed-wing dynamics model.

But the real fixed-wing UAV flight control model is very complex and has strong nonlinearity.
So how to prove that my proposed fixed-wing cooperative control algorithm, or planning algorithm is effective. At this point, it is necessary to use a more realistic fixed-wing flight control to simulate the real UAV flight state. This is the reason why I built this platform.

In fact, Matlab comes with a simulation tool for fixed-wing UAVs, but the official documentation is small, and it is not very convenient to use, and the animation display can only show one aircraft, in short, it is not good.

The code built mainly refers to Randal's "Small Unmanned Aircraft Theory and Practice", which has a flight control code principle that I don't understand at all. My job is to integrate them and  show them inside one screen.

![avatar](picture/small.png)

---

## 3. How to use 

The simulation platform can be divided into two parts, one is the calculation part 'uavA1' and the other is the display part 'uavShow'. 

Just run the main.m file directly.

In fact, you can also synchronize the calculation and display, real-time calculation and then display. But personally, I think this will affect the smoothness of the display.  The more aircraft the greater the impact will be.

### 3.1 Calculation part

The state of each aircraft is calculated in turn over time and will be stored in the x1.mat file (x1 can be x2,x3.... which indicates the number of aircraft).

- CalAlluavs.m 

![avatar](picture/1.png)

### 3.2 Show part

- ShowAlluavs.m 

The data of each aircraft is stored in x, path, waypoint data. Using all the data, the show part could work.


## 4. How to read path files

The folder 'data' provides some path files for 5 aircraft that can be used.

If you want to calculate your own route data, you can follow these steps.
1. uavA1/getWpp.m     -> load '5jia.mat'
2. uavA1/para_chap1.m -> load '5jia.mat'

Find the corresponding code in the file and change the name of '5jia.mat' .

'getWpp.m'  Read the path

'para_chap1.m' reads the initial position of the aircraft

The simulink time needs to be adjusted according to the length of your path file, if your uav obviously did not run through your path, you need to adjust the time longer.

## 5. How to increase the number of uavs

 How to increase the aircraft is actually very easy but a little bit of boring. You need to add some code and change the corresponding numbers. The steps are as follows.
 
## The steps are as follows:

### 1. main.m
First of all, in the 'main.m' file, you can see that the code statements for each aircraft are obvious, add the corresponding sentences. 

![avatar](picture/4.png)

### 2. uavShow/drawEnvironments5.m

Add the sentence of uavShow/drawEnvironments5.m. The sentence here looks complicated, but you don't have to figure out what it means. Just add it mechanically and change the numbers. 
If you look at the file uavShow/drawEnvironments5.m, you'll see what I'm talking about.

![avatar](picture/5.png)

---

![avatar](picture/6.png)

---

![avatar](picture/7.png)

### 3.uavShow/mavsim_show.slx

Open the uavShow/mavsim_show.slx file, simply add a few boxes and then just connect them.

For example, if you want to add the sixth uav, add four boxes: x6, time, path6, waypoints6, and then line them up behind each other.

![avatar](picture/3.png)

--------

