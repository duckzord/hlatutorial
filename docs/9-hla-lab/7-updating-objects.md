---
sidebar_position: 10
---

# Lab 7: Updating Objects

In this lab we will study the services used for sending updates for attributes of objects as well as for reflecting these attributes in subscribing federates.

## Study and verify declarations
In the first lab you have learned how to start and run the federation. As part of this lab you could see cars in the MapViewer (subscriber) that were simulated by the CarSims (publishers).
Do the following:
1. Start up the RTI and all federates. Load a scenario and start simulating.
2. Verify that you can see the cars moving in the MapViewer.
3. In the pRTI user interface: select the CarSimC federate and switch on tracing
of RTI calls and callbacks. You may consider switching off the tracing after a few seconds to limit the number of trace printouts.
4. Look at the CarSimC window. Study the calls that the federate makes to Update Attribute Values service.
5. In the pRTI user interface: select the MapViewer federate and switch on
tracing of RTI calls and callbacks. You may consider switching off the tracing after a few seconds to limit the number of trace printouts.
6. Look at the MapViewer window. Study the Reflect Attribute Value callbacks that the RTI makes to the federate.
7. Terminate the federation.

## A look at source code and APIs
Do the following:
1. Open the CarSim Source code (C++ or Java of your choice). Look at the following classes:
- CarSimJ: se.pitch.hlatutorial.carsim.hlamodule.HLAinterfaceImpl
- CarSimC: /source/HLAmodule.cpp

Locate the code that performs the Update Attribute Values calls and the Reflect Attribute Value callbacks. Note the exception handling which, for clarity, has not been included in the pseudo code in the main text of this tutorial.

2. Locate and study these three services in the HLA Evolved APIs (Doxygen and JavaDoc above).
3. If you have the IEEE 1516-2010.1 specification available, read more about these services in the standard.