---
sidebar_position: 11
---

# Lab 8: Running a Distributed Federation

The following is an advanced exercise for anyone interested in trying out a distributed federation. It assumes that you have at least two computers on a network.

## Running with two computers
We will call the Computer 1 and Computer 2. For simplicity you may need to disable the Windows/Linux firewall on your computers.

We will distribute the applications as follows:

- Computer 1: Central RTI Component, Master, CarSimC
- Computer 2: CarSimJ, MapViewer

1. Make sure that Pitch pRTI Free and the HLA Evolved Starter Kit are installed on both computers.
2. We will use Computer 1 for the Central RTI Component. Start up the Pitch pRTI Free on this computer. Remember the IP address of this computer, for example 192.168.1.23. This address can be located using the “ipconfig” (Windows) or “ifconfig” (Linux) command.
3. Start up the Master and the CarSimC on Computer 1 and verify that they join the RTI.
4. Modify the following files on Computer 2:
- CarSimJ config
- MapViewer config
5. In both of the above files modify the CRChost value to the IP address for computer 1. The resulting line may be for example
- CRChost=192.168.1.23
6. Start the CarSimJ and MapViewer federates on Computer 1.
7. Check in the Pitch pRTI Free user interface that all four federates have joined.
8. Start the simulation using the Master federate.

## Running with even more computers
You may move all federates to different computers. The only requirement is that you have the RTI installed since each federate needs to use the RTI libraries in that installation. You also need to modify the configuration file for each federate so that it connects to the CRC.

## Using the Web View for iPad/Android/iPhone
Read the Pitch pRTI Users Guide on how to start the Web View for Pitch pRTI The Web View enables you to connect to the RTI and manage federations using regular web browsers or tablets (iPad/Android) and even mobile phones.