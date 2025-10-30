---
layout: single
title: "Robot Arm V1"
collection: projects
order: 1
excerpt: "A custom cross functional robotic arm originally for a group project."
header:
  teaser: robot-arm.png
teaser: robot-arm.png        # add this too for compatibility
---


<div class="video-container">
  <iframe
    src="https://www.youtube-nocookie.com/embed/hY593K-q6cw?rel=0&mute=1&autoplay=0&modestbranding=1&playsinline=1"
    title="Robot Arm Test!"
    loading="lazy"
    frameborder="0"
    allow="accelerometer; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share"
    allowfullscreen>
  </iframe>
</div>

## Project: 6-DoF Robotic Arm
---
The robot arm was a group project with four other students. 
Our goal was to build a robotic arm capable of mixing and serving drinks on demand within an eight-week timeframe.
I was responsible for mechanical design, fabrication, and electronics planning throughout the project.
Some of my responsibilities included:
- Estimated load conditions and calculated optimal gearing to ensure motor performance and electronics reliability
- Modeled the robotic system in Fusion 360, accounting for performance requirements, fabrication limitations, and material availability
- Fabricated a 3-DoF robotic arm prototype using a CNC mill and 3D printers

The work described below is my contribution to the project in detail.



Currently, the first three degrees of freedom (positioning) are complete; the remaining three (end-effector orientation) are still in progress.

![The Robot Arm So Far!]({{ '/images/robot-arm.png' | relative_url }}){:.img-fluid}

## Design Goals and Constraints
---
The following were some goals that were determined during the ideation phase:
- The robot shall be compatible with ROS 2
- The robot should be capable of moving from one end point to the other within one second
- The robot should be capable of holding and moving a 2 kg payload at the end of the arm
- Robot parts shall be manufacturable in house or with purchaseable components
- The robot should have a workspace of 6 feet accross
- The robot shall be capable of holding 16oz of liquid and various small objects
- The robot should fit in a generic kitchen setting

This was the initial task decomposition for the robot:
- Recieve order from user
- Pick up mixing cup
- Move to ingredient location
- Dispense ingredient to mixing cup
- Repeat previous two steps until drink is assembled
- Dispense drink to user

## Subsystems
---
The robot arm is divided into two subsystems:
- The arm: a 3DoF articulated arm.
- The end effector: a quaternion wrist with an integrated vacuum cup gripper (WIP).

### The Robot Arm
---
This subsystem is used to move the end effector between way points to retrieve and dispend ingredients. Since this subsystem has a considerable range, the load requirement is much higher than the end effector subsystem.

3-DoF arm made from aluminum rectangular tubing for structure and carbon-fiber tubing for the arm segments.
The first 3 DoF uses FRC motors since they could provide substantial torque while having a desirable speed. All the motors and gearboxes are mounted towards the base to keep the arm segments light.

![Arm Subsystem]({{ '/images/robot-arm2.PNG' | relative_url }}){:.img-fluid}

### The End Effector (WIP)
---
This subsystem is used to manipulate ingredients.

The end effector (quaternion wrist) uses servos for actuation and two vacuum motors to grasp objects like a mixing cup or ice.

## Design Choices and Methods
---

### Electronics
---
For the higher load subsystem we chose to use FRC motors and controllers, namely the 775pro and TalonFXS, because they are readily available, include a wide range of complimentary components, and deliver substantial torque and speed without breaking the bank.

Additionally, the controllers had many built in features that reduced the work load for us such as built in CAN communication, current sensing and ROS compatibility.



For the end effector, we planned to use servos for actuation and a small vacuum motor for gripping. Servos were selected to reduce workload by eliminating the need for PID tuning and additional hardware.

Below is the rough schematic we followed for the electronics layout:

![The Electronics Schematic!]({{ '/images/electronics-schematic.PNG' | relative_url }}){:.img-fluid}

### Torque Estimation
---
The torque requirement was estimated using static analysis with the highest load estimated at around 40 Nm.

It was assumed that the payload would be 2 kg with a torque arm of 1 meter based on the design goals and constraints.

![FBD]({{ '/images/fbd.PNG' | relative_url }}){:.img-fluid}


### Gearbox Sizing
---
Despite the motors being fairly strong, a gearbox was necessary to achieve the desired output torque and protect upstream electronics from overload.

Torque and RPM at peak power were used for sizing, based on the assumption that the motor would operate near this point while performing work.

![Motor Curve]({{ '/images/motor-curve.png' | relative_url }}){:.img-fluid}

The reduction was calculated based on the goal of traveling from endpoint to endpoint in under one second, 0.5 rps or 60 rpm.

A 20% margin was added to the peak rpm, to provide speed headroom, then divided by the desired 60 rpm resulting in a 187.4:1 desired gear reduction. However, the final reduction was reduced to 120:1 later on since the arm lengths were reduced to meet size constraints. 

$$
Desired RPM = 60 RPM
$$

$$
Peak Power RPM = 9370 RPM
$$

$$
Gear Ratio = \frac{9370 RPM * 1.2}{60 RPM} = 187.4
$$

This gear ratio was then applied to the motor’s theoretical output torque and compared against the estimated requirement of ~40 Nm with a 20% torque margin to confirm that it would meet performance needs with some headroom to account for unexpected loads. Since the available torque is much higher that the required torque, friction was determined to be negligible.

$$
Desired Torque = 40 Nm *1.2 = 48 Nm
$$

$$
Peak Power Torque = 0.3 Nm
$$

$$
Estimated Output Torque = 0.3 Nm * 187.4 = 56.1 Nm
$$

$$
Output > Desired
$$

All three joints of the arm uses the same size gearbox since they all have a torque requirement below the max output torque and can perform a 180 degree rotation under a second.

![Side view of the arm gearbox]({{ '/images/robot-arm3.png' | relative_url }}){:.img-fluid}

### Part Selection
---
In order to meet our deadline, we selected materials that were compatible with the machinery we had access to. Machinery we used included the HAAS TM-1 and some manual mills and lathes.

The main structural aluminum was sourced from the remnant section at Industrial Metal Supply, where we found an 8-foot piece of 6x2-inch 6061 tubing for $40.
The carbon fiber tubes, aluminum round tubing, and bearings were purchased from Amazon.

<div class="video-container">
  <iframe
    src="https://www.youtube-nocookie.com/embed/iHVmGTyaGT8?rel=0&mute=1&autoplay=0&modestbranding=1&playsinline=1"
    title="CNCing!"
    loading="lazy"
    frameborder="0"
    allow="accelerometer; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share"
    allowfullscreen>
  </iframe>
</div>


### Gripper Design
---
We found limited resources on vacuum cup design, so we began by replicating common vacuum cups used in factory automation and iterated from there to meet our needs.

Through several rounds of testing, we found that the optimal design for holding a mixing cup of liquid was a vacuum cup with a large area, no bellows and a thick base to ensure little flexing while holding.

The current design is 3D printed using Flexible 80A resin on a Form 4 printer, though we also experimented with urethane casting during development.

![FBD]({{ '/images/UC.png' | relative_url }}){:.img-fluid}
![FBD]({{ '/images/cuptest.png' | relative_url }}){:.img-fluid}

<div class="video-container">
  <iframe
    src="https://www.youtube-nocookie.com/embed/CAndtVpHk9o?rel=0&mute=1&autoplay=0&modestbranding=1&playsinline=1"
    title="Gripper Testing!"
    loading="lazy"
    frameborder="0"
    allow="accelerometer; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share"
    allowfullscreen>
  </iframe>
</div>

## Additional Photos
---

<div class="masonry" markdown="1">
![Alt 1]({{ '/images/pic1.png' | relative_url }})
![Alt 2]({{ '/images/pic2.png' | relative_url }})
![Alt 3]({{ '/images/pic3.png' | relative_url }})
![Alt 3]({{ '/images/pic4.PNG' | relative_url }})
![Alt 3]({{ '/images/pic5.png' | relative_url }})
</div>
