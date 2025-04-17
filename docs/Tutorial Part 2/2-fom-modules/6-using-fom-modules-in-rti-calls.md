---
sidebar_position: 4
---

# The Federation Object Model (FOM)

We will now see how the modules get loaded. It is actually quite simple. Just specify the list of modules when you create the federation execution.

```rti.createFederationExecution(“MyFederation”, [“FederationManagement”, “FuelEconomy”])```

The RTI will provide the MIM for you automatically so you should not include it in the list of modules. The order of the modules doesn’t matter. In case there is a conflict between modules in the list or if some of the modules are incorrect the load of the entire list of modules will fail.

The switches table must be included in at least one of the FOM modules used when creating the federation execution. In this case it is included in the Fuel Economy module.

You may also provide FOM modules when joining a federation, thus extending the FOM modules in a federation during the simulation. This is a more advanced approach and it is not covered in this tutorial.
