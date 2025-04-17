---
sidebar_position: 7
---

# Lab 4: Sending and Receiving Interactions

In this lab we will study the services used for sending and receiving interactions.
## Study and verify declarations

Follow these steps:
1. Start the RTI (CRC)
2. Start the Master federate. Look at the pRTI user interface. Select the Master federate and look at the Declarations
3. You should see that the Start, Stop and LoadScenario interactions are Published. The ScenarioLoaded and ScenarioLoadFailure interactions should be Subscribed.
4. Start the CarSimC federate. Look at the pRTI user interface. Select the CarSimJ federate and look at the Declarations
5. You should see that the ScenarioLoaded and ScenarioLoadFailure interactions are Published. The Start, Stop and LoadScenario interactions should be subscribed


## Study and verify send and receive services
Follow these steps:
1. In the Master federate, give a LoadScenario command which initiates a LoadScenario interaction.
2. Look at the CarSimC federate and see that it prints a message that it received the interaction.
3. When the CarSimC federate has loaded the scenario it will send a ScenarioLoaded interaction. Look at the Master federate and verify that it
prints a message that it has received the interaction.
4. Advance users may switch on the trace for a federate in the RTI user interface.
5. Shut down the federation

## A look at source code and APIs
Do the following:

1. Open the CarSim Source code (C++ or Java of your choice). Look at the following classes:
- CarSimJ: se.pitch.hlatutorial.carsim.hlamodule.HLAinterfaceImpl
- CarSimC: /source/HLAmodule.cpp

Locate the code that performs the Get Interaction Class Handle and Send Interaction calls and that implements the Receive Interaction callback. Note the exception handling which, for clarity, has not been included in the pseudo code in the main text of this tutorial.

2. Locate and study these three services in the HLA Evolved APIs (Doxygen and JavaDoc above).

If you have the IEEE 1516-2010.1 specification available, read more about these services in the standard.