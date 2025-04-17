---
sidebar_position: 2
---

# A Look Back at Part One

Welcome to the HLA Tutorial part two. In part one we have covered the basic services that most HLA federates use. This includes
 
- Connecting to the RTI, creating a federation execution and joining it
- Publishing and subscribing interactions and object classes with attributes
- Encoding and decoding data 
- Sending and receiving interactions
- Registering and discovering object instances
- Updating and reflecting attribute values. 

All information exchange is based on the Federation Object Model (FOM) that we developed. The most commonly used parts of the FOM are 

- Objects with attributes, 
- Interactions with parameters. 
- For attributes and parameters we also need to define data types. 
- In addition to this we describe the purpose, author, version and other meta-information in the Identification table. 

Using the FOM and the RTI services we are able to achieve a number of things including:

- Exchange of car data
- Execution management, i.e. starting and stopping
- Scenario management, in this case simply selecting a scenario stored on file

The overall design of the federation is captured in a Federation Agreement. The FOM is a part of the Federation Agreement. 

Not only did we cover the use of a number of HLA services. We also showed one typical way to build distributed simulations, namely:

- The HLA interface of an application is usually separated into a dedicated module.
- A dedicated federate is used to control the federation, both the scenario and the execution.
- Some federates may be dedicated to just subscribing to information and visualize the simulated processes
- A federate that can simulate one instance of an object class, such as a car, can usually simulate several instances.
- There may be several federates that simulate the same processes and publishes the same object and interaction classes.
- A federate is often initialized with parameters for the models upon startup.
- Part of the scenario may be centrally managed but scenario data that is only meaningful to some particular federate may be locally managed.
