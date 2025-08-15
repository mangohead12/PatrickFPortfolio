---
title: "Robot Arm (WIP)"
order: 1
excerpt: "A custom cross functional robotic arm originally for a group project."
header:
  image: images/robot-arm.png
  teaser: images/robot-arm.png

collection: projects
---


## Project: 6-DoF Robotic Arm
The robot arm was a group project with four other students. 
The goal was to create a robotic arm with the goal of making mixed drink to order within a 8 week period. 
I was responsible for mechanical design, fabrication, and electronics planning throughout the project.
Some of my resposibilities included the following:
- Estimate load conditions and calculate ideal gearing to ensure motor capability and electronics reliability
- Model the robotic system in Fusion 360 considering performance requirements, fabrication limitations and material availability
- Fabricated a 3 DoF robot arm prototype using a CNC mill and various 3D printers

The work described below is my contribution to the project in detail.

As of now, the first three degrees of freedom (positioning) are complete, while the remaining three degrees (end-effector for orientation) are still in progress.

![The Robot Arm So Far!]({{ '/images/robot-arm.png' | relative_url }}){:.img-fluid}

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

---

<details open markdown="1">
  <summary><strong>The Design</strong></summary>

## Design Goals
The following were some goals that were determined during the ideation phase:
- The robot shall be compatible with ROS2
- The robot should be capable of moving from one end point to the other within one second
- The robot should be capable of holding and moving a 2 pound payload at the end of the arm
- Robot parts shall be manufacturable in house or purchaseable online
- The robot should have a workspace of 6 feet accross
- The robot shall be capable of holding 16oz of liquid and various small objects
- The robot should fit in a generic kitchen setting

## Subsystems
The robot arm is divided into two subsystems:
-The arm: a 3DoF articulated arm.
-The end effector: a quaternion wrist with an integrated vacuum cup gripper (WIP).

### The Robot Arm
The robot arm is a 3 DoF arm made of aluminum rectangular tubing for the structure and carbon fiber tubes for the arms.
The first 3 DoF uses FRC motors since they could provide substantial torque while having a desirable speed. All the motors and gearboxes are mounted towards the base to keep the arm segments light.

![Arm Subsystem]({{ '/images/robot-arm2.PNG' | relative_url }}){:.img-fluid}

### The End effector
The end effector (quaternion wrist) uses servos for actuation and two vacuum motors to grasp objects like a mixing cup or ice.



</details>

---

<details open markdown="1">
  <summary><strong>Design Choices and Design Methods</strong></summary>

## Electronics
For the higher load subsystem we chose to use FRC motors and controllers, namely the 775pro and TalonFXS, because they are readily available, include a wide range of compatible components, and deliver substantial torque and speed without breaking the bank.

Additionally, the controllers had many built in features that reduced the work load for us such as built in CAN communication, current sensing and ROS compatability.

For the end effector, we planned to use servos for the acuations and a small vacuum motor for gripping. Servos were selected since were wanted to reduce the workload by eliminated PID tuning and additional hardware.

Below is the rough schematic we followed for the electronics layout:

![The Electronics Schematic!]({{ '/images/electronics-schematic.PNG' | relative_url }}){:.img-fluid}

## Torque Estimation
The estimated torque requirement was estimated using static analysis with the highest load estimated at around 40 Nm.

Since this was before the final design was complete, it was assumed that the payload would be around 2 kg with a torque arm of 1 meter.

![FBD]({{ '/images/fbd.PNG' | relative_url }}){:.img-fluid}


## Gearbox Sizing
Although the motors are fairly strong, a gearbox was necessary to achieve the desired output torque and protect upstream electronics from overload.

Torque and RPM at peak power were used for sizing, based on the assumption that the motor would operate near this point under load.

![Motor Curve]({{ '/images/motor-curve.png' | relative_url }}){:.img-fluid}

The reduction was calculated based on the goal of traveling from endpoint to endpoint in under one second.

A 20% margin was added to the peak rpm then divided by the desired 60 rpm resulting in a 187:1 desired gear reduction. However, the final reduction was reduced to 120:1 to match the shortened arm lengths while maintaining ample torque.

$$
Desired RPM = 60 RPM
$$

$$
Peak Power RPM = 9370 RPM
$$

$$
Gear Ratio = \frac{9370 RPM * 1.2}{60 RPM} = 187.4
$$

This gear ratio was then applied to the motor’s theoretical output torque and compared against the estimated requirement of ~20 Nm to confirm that it would meet performance needs.

$$
Desired Torque = 40 Nm
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

All three joints of the arm uses the same size gearbox since they all have a torque requirement below the max output torque and can perform a 180 degree rotation under a second and have a torque requirement below the max output torque.

![Side view of the arm gearbox]({{ '/images/robot-arm3.png' | relative_url }}){:.img-fluid}

## Part Selection
In order to meet our deadline, we selected materials that were available and were compatible with the machinery we had access to. Some machinery we used included the HAAS TM-1 and some manual mills and lathes.

The main structural aluminum was sourced from the remnant section at Industrial Metal Supply, where we found an 8-foot piece of 6x2-inch 6061 tubing for $40.
The carbon fiber tubes, aluminum round tubing, and bearings were purchased from Amazon, chosen for their convenient sizes and affordability at the time.

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


## Gripper Design
We found limited resources on vacuum cup design, so we began by replicating common vacuum cups used in factory automation and iterated from there.

Through several rounds of testing, we found that the optimal design for holding a large cup of liquid was a cup with a large area, no bellows and a thick base to ensure little flexing while holding.

The current design is 3D printed using Flexible 80A resin on a Form 4 printer, though we also experimented with urethane casting during development.

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

</details>

## Additonal Photos
<div class="masonry" markdown="1">
![Alt 1]({{ '/images/pic1.png' | relative_url }})
![Alt 2]({{ '/images/pic2.png' | relative_url }})
![Alt 3]({{ '/images/pic3.png' | relative_url }})
![Alt 3]({{ '/images/pic4.PNG' | relative_url }})
![Alt 3]({{ '/images/pic5.png' | relative_url }})
</div>
