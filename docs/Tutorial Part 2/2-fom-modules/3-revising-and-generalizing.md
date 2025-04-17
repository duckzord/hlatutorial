---
sidebar_position: 3
---

# 2.3.	Revising and Generalizing a Module

In case a module needs to be reusable it also needs to have some degree of generality. To make it extremely reusable there is a risk that I might become very abstract, which makes it harder to use. Just like any software design this is all about striking a balance!

We will now do three things:

1. Remove the InitialFuelAmount parameter from the LoadScenario interaction. Since it now only uses one parameter, the scenario name, we will rename it LoadNamedScenario for clarification.
2. We will introduce a new interaction called “SetScenarioParameters” in the Federation Management module. This parameter can be called after loading the scenario to set additional scenario parameters. Note that it has no actual parameters
3. We will create a subclass of this new interaction called SetFuelParameters in the Fuel Economy FOM module. This interaction has an InitialFuelAmount parameter.

Here is the new result:

![interactions.png](img%2Finteractions.png)

| **Interaction classes (with parameters)** | **Data types**        |
|-------------------------------------------|-----------------------|
| LoadScenario                              | ScaleFactorFloat32    |
|                                           | SetScenarioParameters |
|                                           | ScenarioLoaded        |
|                                           | ScenarioLoadFailure   |
|                                           | Start                 |
|                                           | Stop                  |

![load-scenario.png](img%2Fload-scenario.png)
	
| **Object classes (with attributes)** | **Interaction classes**                 | **Data types** |
|--------------------------------------|-----------------------------------------|----------------|
| Car                                  | SetScenarioParameters.SetFuelParameters | FuelInt32      |
|                                      |                                         | AngleFloat64   |
|                                      |                                         | PositionRec    |
|                                      |                                         | FuelTypeEnum32 |

Note that the Fuel Economy module is now dependent on the Federation Management module since it introduces a subclass to SetScenarioParameters. Technically you could have sipped the SetScenarioParameters but this would have made the pattern, introduced in the Federation Management module, less clear. Here are the dependencies between the FOM Modules Fuel Economy, Federation Management and the MIM.

![dependencies.png](img%2Fdependencies.png)

It is common to have several modules depend on one particular module. In our example both Fuel Economy and Federation Management uses concepts from the MIM.

It is also not uncommon for one module to depend upon several other modules. Fuel Economy uses concepts from both the MIM and the Federation Management.

(There is a rule for good design for C++ and Java packages that also applies here: There should be no circular dependencies in the module dependency graph. We should avoid having Federation Management dependent on Fuel Economy.)

