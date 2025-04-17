---
sidebar_position: 2
---

# Splitting the Fuel Economy Federation FOM

The first thing we need to do when using FOM modules is to specify exactly what is the purpose of a FOM module and what is the intended degree of reuse. In this case the modules will be:
- A general Federation Management module for handling scenario and starting and stopping. It should be possible to reuse this module across several other federations that may simulate other things than cars.
- A specific Fuel Economy module for Cars. It shall solve the specific needs of this federation. This will probably make it less reusable across other federations.

In our first attempt the following things will go into the Federation Management module:

| **Interaction classes (with parameters)** | **Data**           |
|-------------------------------------------|--------------------|
| LoadScenario                              | ScaleFactorFloat32 ||
| ScenarioLoaded                            |                    |
| ScenarioLoadFailure                       |                    |
| Start                                     |                    |
| Stop                                      |                    |

The following things will go into the Fuel Economy module:

|**Object classes (with attributes)**|**Data types**|
|---|---|
|Car|FuelInt32|
||AngleFloat64|
||PositionRec|
||FuelTypeEnum32|
 
There are however a few issues here. Do you remember the LoadScenario interaction?

![load-scenario.png](img%2Fload-scenario.png)

There is a parameter called InitialFuelAmount in the LoadScenario interaction. We have specified that the Federation Management module shall be reusable and not tied to the Fuel Economy module. Obviously this parameter contradicts this.

