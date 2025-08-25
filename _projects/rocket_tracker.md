---
title: "Rocket Tracker"
order: 3
excerpt: "A turret to point a yagi antenna at a rocket during flight."
collection: projects
---

![Rocket tracker]({{ '/images/tracker.png' | relative_url }}){:.img-fluid}

### Situation
This project was for the liquid rocketry club at the University of California, Riverside. The goal of this project was to develop support equipment to receive throughout flight and descent of a amateur liquid rocket launch.

Since everyone is required to remain inside bunkers throughout the launch and landing, the club wanted to develop equipment to keep a yagi antenna pointed the rocket through flight and landing to receive live data such as propellant pressure. 

The Design constraints were as follows:
-  The system shall move a payload of 500 grams
-  The system shall be capable of pointing to any point in a hemisphere
-  The system shall cost less that $100 in total
-  The system shall mount to the end of a 10 ft pole

Through a few whiteboarding sessions, it was determined to be the best balance between effectiveness and cost since the wrist could output twice the amount of torque and was mechanically simpler compared to other ideas generated.



Below is the proof of concept prototype. Because motors from an old 3D printers were used, the there were no available motor curves to perform calculations. For future iterations it was planned to upgrade to stronger motors. 

The prototype was wired up and coded using an Arduino and tmc2208 stepper motor drivers. The plan for tracking the rocket was to use computer vision to follow the rocket on the way up and the parachute on the way down however this project was ultimately put on hold to prepare the rocket for launch. 

![Rocket tracker]({{ '/images/tracker.png' | relative_url }}){:.img-fluid}
![Rocket tracker]({{ '/images/tracker2.PNG' | relative_url }}){:.img-fluid} 

