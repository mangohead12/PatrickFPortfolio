---
title: "Straw Bridge Challenge"
order: 4
excerpt: "A straw bridge design challenge as part of the final project for the machine design course"
collection: projects
---

![Bridge]({{ '/images/bridge.PNG' | relative_url }}){:.img-fluid}

The final project for Machine Design was a challenge to design, build and test straw bridges. Grades were based on failure load prediction and performance efficiency compared to the class average. My group ended up scoring the highest efficiency ever in the class's history with an efficiency of 732%. Our success was attributed performing several iterations of simulation to find the most effecient design while building several prototypes to ensure the best build quality. 

### Design Approach
To find the ideal bridge design, we considered creating spreadsheet calculators to find the stress in every member using method of sections and finding the critical load using the column buckling equation but realized that it would take more time to update the calculator for additional nodes so we shifted towards simulating various designs with FEA. Some members in the group used ANSYS and Solidworks while I used Fusion 260 to ensure accurate predictions. 

![Bridge]({{ '/images/bridgesim.PNG' | relative_url }}){:.img-fluid}

### Assembly Methods
During testing, we quickly realized that inconsistencies in glue joints and the squareness of members greatly reduced the performance of our bridges since it lead to failure modes that occur before column buckling. 

I created several 3D printed jigs to assist with the assembly process and straw cutting.

Our final bridge held a load of 8 kg and weighed 10 grams!


![Bridge]({{ '/images/bridgejig.png' | relative_url }}){:.img-fluid}
![Bridge]({{ '/images/bridgejig2.PNG' | relative_url }}){:.img-fluid}
