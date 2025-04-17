---
sidebar_position: 7
---

# Running HLA Time Management in the CarSim Federates

Let’s look at the main loop of the CarSim federate. We will need to ask permission from the RTI before advancing to the next time step. The RTI will grant us the permission to move to our next time step when this is acceptable to the federation.

This means that the main loop in the simulation will actually contain of two distinct phases, as shown in the picture 6-7.

![7-granted-sequence.png](img%2F7-granted-sequence.png)

1.	**Granted**. In this phase we have been granted to a new logical time by the RTI. We can now calculate and produce updates for this logical time.
2.	**Advancing**. In this phase we are requesting the permission from the RTI to advance to a new time. We also promise that the federate will not produce any updates or interactions for the requested logical time. During this time we will receive updates and interactions with the requested logical time from other federates.
 
The main simulation loop will contain code that requests time advance. This is what the code may look like.

``` java
_grant = false;
HLAinteger64Time tNext = _tCurrent.add(_step)
_rtiAmbassador.timeAdvanceRequest(tNext);
 	while (!_grant) {
        	// Process incoming messages
		Thread.sleep(10);
    	}
     	// Time has now been advanced
```

Here is the callback that grants us permission to the requested time.
 	 
``` java
void timeAdvanceGrant(LogicalTime t)  // Callback
{
    _tCurrent = (HLAinteger64Time)t;
    _grant = true;
}
```
When you send updates you must now be careful to provide the logical time for which the update is valid. In the CarSim example this is the current time plus the length of the time step.

``` java
 _rtiAmbassador.updateAttributeValues(
  		carInstanceHandle, attributes, userSuppliedTag, tNext);
```
  		

A timestamp is also delivered in the corresponding reflect attribute values callback.

``` java
`reflectAttributeValues(objectHandle, attributeValueMap, timestamp)
{
    HLAinteger64Time tReflected = (HLAinteger64Time)timestamp;
}`
```

The CarSims can now interoperate with the simulation data perfectly time synchronized, no matter how fast or slow the simulations run or if there are differences in computer clock speed or calibration. The simulation will be deterministic and repeatable.
