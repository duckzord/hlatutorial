---
sidebar_position: 2
---

# Designing DDM in a Federation

When implementing DDM in a federation we need to decide on the following:

- Exactly **what information** (attributes, interactions) do we want to filter? 
- On **what criteria** do we want to filter? Type of fuel? Position?

In the Fuel Economy Federation we want to be able to filter all attributes of a car, i.e. we either get all the information about a particular car or we get no information about the car. We want to filter on two properties: the type of fuel of the car and the location of the car, as described using Latitude and Longitude.

Filtering will be done using **DDM Dimensions**. We will start with one dimension for Fuel Type in this case, which we call FuelTypeDim. Here is a first summary of how it will be used:


| Object Class | Attribute          | Filter on FuelTypeDim |
|--------------|--------------------|-----------------------|
| Car          | Name               | Yes                   |
|              | LicensePlateNumber | Yes                   |
|              | FuelLevel          | Yes                   |
|              | FuelType           | Yes                   |
|              | Position           | Yes                   |

It is recommended to filter all of the attributes of a particular class in the same way, unless you have very special requirements. It is of course also possible to use DDM to filter interactions classes.

The use of DDM must be clearly defined and shared between all developers in the federation so that it is correct and consistent across the federation, using the FOM and the Federation Agreement. In particular, we need to define how the DDM information should be calculated from the simulation data. This is called the Normalization Function, as shown in Figure 7-2. 

![2-normalization.png](img%2F2-normalization.png)

We may want to filter on many types of information: enumerations, integers or floating point values. We may also want to use information from any variable: an attribute or parameter in the FOM or some data that is internal to a simulator. When passed to the RTI we use the Normalization Function to convert it to integer-based Regions that the RTI can use. It is up to the federate developer to develop the code that implements the normalization function.
