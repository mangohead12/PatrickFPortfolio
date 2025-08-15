---
title: "Robot Arm (WIP)"
order: 1
excerpt: "Short description of portfolio item number 1<br/><img src='/images/500x300.png'>"
collection: projects
---

## Project: 6-DoF Robotic Arm
The robot arm was a group project with four other students. 
The goal was to create a robotic arm with the goal of making mixed drink to order within a 13 week period. 
I was responsible for mechanical design, fabrication, and electronics planning throughout the project.

As of now, the first three degrees of freedom (positioning) are complete, while the remaining three degrees (end-effector for orientation) are still in progress.

![The Robot Arm So Far!](/assets/images/Robot-Arm.png)

---

<details>
  <summary><strong>The Design</strong></summary>

## Design Goals
The following were some goals that were determined before the design phase:
- The robot shall be compatible with ROS2
- The robot should be capable of moving from one end point to the other within one second
- The robot should be capable of holding and moving a 2 pound payload at the end of the arm
- Robot parts shall be manufacturable in house or purchaseable online
- The robot should have a workspace of 6 feet accross
- The robot shall be capable of holding 16oz of liquid and various small objects

## Subsystems

The robot arm is divided into two subsystems:
-The positional: a 3DoF articulated arm
-The orientation subsystem: a quaternion wrist with an integrated vacuum cup gripper (WIP).

The first 3 DoF uses FRC motors since the torque requirement is higher than the hobbyist motors I found online. All the motors and gearboxes are mounted towards the base to keep the arm segments light.

The end effector (quaternion wrist) uses servos for actuation and two vacuum motors to grasp objects like a mixing cup or ice.

</details>

---

<details>
  <summary><strong>Design Choices and Design Methods</strong></summary>

## Electronics
Due to time constraints, many decisions were made quickly, and while effective, some may not have been optimal in hindsight.

We chose to use FRC motors and controllers because they are readily available, include a wide range of compatible components, and deliver substantial torque without the need for industrial-grade hardware.

We also opted for CAN communication to provide better flexibility in integration and control of the motor systems.

Here’s the rough schematic we followed for the electronics layout:

![The Electronics Schematic!](/assets/images/Electronics-Schematic.png)


## Gearbox Sizing
Although the motors are fairly strong, a gearbox was necessary to achieve the desired output torque and protect upstream electronics from overload.

Torque and RPM at peak power were used for sizing, based on the assumption that the motor would operate near this point under load.

The reduction was calculated based on the goal of traveling from endpoint to endpoint in under one second.

A 20% margin was added to the peak rpm then divided by the desired 60 rpm resulting in a 187:1 desired gear reduction. However, the final reduction was reduced to 120:1 to match the shortened arm lengths while maintaining ample torque.

$$
Gear Ratio = \frac{9370 * 1.2}{60} = 187.4
$$

This gear ratio was then applied to the motor’s theoretical output torque and compared against the estimated requirement of ~20 Nm to confirm that it would meet performance needs.

$$
some equation
$$

All three joints of the arm uses the same size gearbox since they all have a torque requirement below the max output torque and can perform a 180 degree rotation under a second.

## Part Selection
Many of the components for the robot were selected spontaneously based on availability and cost.

The main structural aluminum was sourced from the remnant section at Industrial Metal Supply, where we found an 8-foot piece of 6x2-inch 6061 tubing for $40.
The carbon fiber tubes, aluminum round tubing, and bearings were purchased from Amazon, chosen for their convenient sizes and affordability at the time.

## Gripper Design
We found limited resources on vacuum cup design, so we began by replicating common vacuum cups used in factory automation and iterated from there.

Through several rounds of testing, we found that the optimal design for holding a large cup of liquid was a cup with a large area, no bellows and a thick base to ensure little flexing while holding.

The current design is 3D printed using Flexible 80A resin on a Form 4 printer, though we also experimented with urethane casting during development.


</details>
