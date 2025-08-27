---
title: "Straw Bridge Challenge"
order: 4
excerpt: "A straw bridge design challenge as part of the final project for the machine design course"
collection: projects
---

![Bridge]({{ '/images/bridge.PNG' | relative_url }}){:.img-fluid}

The final project for Machine Design was a challenge to design, build and test straw bridges. Grades were based on failure load prediction and performance efficiency compared to the class average. My group ended up scoring the highest efficiency ever in the class's history with an efficiency of 732%. Our success was attributed performing several iterations of simulation to find the most efficient design while building several prototypes to ensure the best build quality. 

### Design Approach
We initially considered using spreadsheet-based calculators (method of joints + buckling equations) to estimate stress and critical loads, but updates became time-consuming. Instead, we switched to FEA tools, namely ANSYS, SolidWorks simulation, and Fusion 360, which allowed faster iteration and accurate predictions.

![Bridge]({{ '/images/bridgesim.PNG' | relative_url }}){:.img-fluid}

### Assembly Methods
During testing, we quickly realized that inconsistencies in glue joints and the squareness of members greatly reduced the performance of our bridges since it led to failure modes that occur before column buckling. 

I created several 3D printed jigs to assist with the assembly process and straw cutting.

Our final bridge held a load of 8 kg and weighed 10 grams!


![Bridge]({{ '/images/bridgejig.png' | relative_url }}){:.img-fluid}
![Bridge]({{ '/images/bridgejig2.PNG' | relative_url }}){:.img-fluid}
