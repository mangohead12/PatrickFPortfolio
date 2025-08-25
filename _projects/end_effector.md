---
title: "Fruit Picking End Effector"
order: 2
excerpt: "Short description of portfolio item number 1<br/><img src='/images/500x300.png'>"
collection: projects
---

<div class="video-container">
  <iframe
    src="https://www.youtube-nocookie.com/embed/auz7zTZCZwE?rel=0&mute=1&autoplay=0&modestbranding=1&playsinline=1"
    title="End effector demo!"
    loading="lazy"
    frameborder="0"
    allow="accelerometer; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share"
    allowfullscreen>
  </iframe>
</div>

This project was my contribution to the Robotics and Medical Systems Lab at the University of California, Riverside as an undergraduate researcher. 

### Context

One of the ongoing projects of the research group is an agricultural robot that can access the interior of tree canopies to harvest fruits. My task was to design an end effector to twist and pull fruit from their stems once the arm continuum arm section of the robot is positioned below the target fruit. The figure below demonstrates the existing system that I am designing around. 

![Cont Robot Arm]({{ '/images/continuum.PNG' | relative_url }}){:.img-fluid}

My design contraints were derived from the existing robot arm:
- The end effector should weigh less than 100 grams
- The end effector shall grasp fruit with a vacuum cup
- The end effector shall twist and pull to harvest the target
- The end effector shall fit within the cross section of the continuum arm

### Ideation

My initial approach towards converging on a mechanism was to create rough models in Fusion 360 and evaluating efficacy from there.

#### Pin Slot Mechanism
Using a platform with bearings that ride on a slotted helical path to achieve simulataneous twisting and pulling

The size of the mechanism left little room for adjustment and fine tuning

<div class="video-container">
  <iframe
    src="https://www.youtube-nocookie.com/embed/351bTEg0328?rel=0&mute=1&autoplay=0&modestbranding=1&playsinline=1"
    title="Pin Slot"
    loading="lazy"
    frameborder="0"
    allow="accelerometer; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share"
    allowfullscreen>
  </iframe>
</div>

#### Lead Screw Mechanism
A platform mounted to a central ball screw. 

This idea required a lot of hardware that was expensive and heavy for the size

<div class="video-container">
  <iframe
    src="https://www.youtube-nocookie.com/embed/_ooPPNEGIHs?rel=0&mute=1&autoplay=0&modestbranding=1&playsinline=1"
    title="Ball Screw"
    loading="lazy"
    frameborder="0"
    allow="accelerometer; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share"
    allowfullscreen>
  </iframe>
</div>

#### Parallel Platform
A platform connected to three parallel linkages that pull and twist the platform

This idea was mechanically complicated and had several high stress parts, specifically the linkages

<div class="video-container">
  <iframe
    src="https://www.youtube-nocookie.com/embed/AtYT0v4jE3Q?rel=0&mute=1&autoplay=0&modestbranding=1&playsinline=1"
    title="Twisting Platform"
    loading="lazy"
    frameborder="0"
    allow="accelerometer; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share"
    allowfullscreen>
  </iframe>
</div>

### The Final Design
#### Actuator Design
While taking a different approach by decomposing the twisting and pulling into seperate motions, I came up with a cable driven mechanism that would achieve the two motions seperately. 

This design was evaluated to be the most promising of the ideas since it was compact and lightweight with room for adjustment.

![Arm Subsystem]({{ '/images/picker1.PNG' | relative_url }}){:.img-fluid}
![Arm Subsystem]({{ '/images/picker2.PNG' | relative_url }}){:.img-fluid}

The figures above serves as a visual demonstration of the working principle of the actator. 
The left column shows the end effector at its starting position after grasping the target fruit.
In the middle column, the actuation string is pulled so that central drum turns to twist the target fruit. 
As the string is fully unwound from the central drum, the string begins pulling downwards on the platform that houses the drum which pulls the target away from its branch.

### Gripper Design


