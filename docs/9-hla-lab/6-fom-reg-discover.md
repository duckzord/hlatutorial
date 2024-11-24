---
sidebar_position: 9
---

# Lab 6: Registering and Discovering Object Instances

In this lab we will study the services used for registering and discovering object instances.

## Study and verify declarations
Follow these steps:
1. Start the RTI (CRC)
2. Start the Master federate. Then start the CarSimC and the MapViewer federate. Look at the pRTI user interface. Select the CarSimC federate and look at the Declarations
3. You should see that the Car object class (including all of the attributes) is Published.
4. Start the MapViewer federate. Look at the pRTI user interface. Select the MapViewer federate and look at the Declarations
5. You should see that the Car object class subscribed

## Study and verify registration and discovery services
Follow these steps:
1. In the Master federate, give a LoadScenarion command.
2. Look in the pRTI GUI at the Fuel Economy federation. Look at the Object Instances of the federation. You should now see the Car instances that have been registered in the federation
3. Look in the pRTI GUI at the CarSimC federate. Look at Known Instances and verify that the cars are known (actually created) by this federate.
4. Look in the pRTI GUI at the MapViewer federate. Look at Known Instances and verify that the cars are known (actually discovered) by this federate.
5. Shut down the federation

## A look at source code and APIs
Do the following:
1. Open the CarSim Source code (C++ or Java of your choice). Look at the following classes:
- CarSimJ: se.pitch.hlatutorial.carsim.hlamodule.HLAinterfaceImpl
- CarSimC: /source/HLAmodule.cpp

Locate the code that performs the Register Object Instance call and that implements the Discover Object Instance callback. Note the exception handling which, for clarity, has not been included in the pseudo code in the main text of this tutorial.

2. Locate and study these three services in the HLA Evolved APIs (Doxygen and JavaDoc above).
3. If you have the IEEE 1516-2010.1 specification available, read more about these services in the standard.