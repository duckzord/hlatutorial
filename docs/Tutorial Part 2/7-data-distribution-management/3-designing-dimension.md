---
sidebar_position: 3
---

# Design DDM in a Federation

First of all, we want to be able to subscribe only to cars that are powered by gasoline, diesel or some other type of fuel. We will now design the FuelTypeDim dimension. A DDM dimension is based on positive integer values, starting on zero. The DDM information is provided by federates as DDM Regions. We use regions when updating attributes. We also use it when subscribing to attribute values. Figure 7-3 describes some sample regions that are useful in the Fuel Economy Federation.

![3-sample-regions.png](img%2F3-sample-regions.png)

When we send attribute updates for a diesel car we can include DDM information that this information relates to a diesel car by providing the region called “Diesel” in the left part of Figure 7-3. This Region consists of one Range: [1..2), which means that “1” is included in the range but not “2”. This is also called a Point Range (due to the size being one unit) with the value “1”.

When we subscribe to attribute updates we can include DDM information that we are only interested in diesel and natural gas cars by providing two regions “Diesel” and “Natural Gas”. These two Region consists of the Ranges: [1..2) and [3..4) respectively. Later on we will see how the RTI uses this information to filter by checking for overlap between the DDM information for updates (shown on the left side of the figure) and subscription (shown on the right side of the figure).

Figure 7-4 illustrates how values with the FuelTypeEnum32 datatype are normalized into the FuelTypeDim dimension.

![4-fuelTypeDim-normalized.png](img%2F4-fuelTypeDim-normalized.png)

To the left we can see FuelTypeEnum32, the HLA datatype that the dimension is based upon. To the right we can see the range of normalized values. These are integers, starting with zero and up to, but not including 4. The value 4 is called the Dimension Upper bound (DUB). In the middle we can see the normalization function that is used for converting data of the specified datatype to a normalized value. This case is extremely simple since the FuelTypeEnum32 uses an integer between 0 and 3, and the normalized values are integers between 0 and 3. We simply use the same value. This case may seem simple, but the normalization functions later in this chapter are less trivial.

Figure 7-5 shows the definition of the FuelTypeDim in the FOM

![5-fom-subscribe-with-ddm.png](img%2F5-fom-subscribe-with-ddm.png)

This definition specifies the following:

- The name of the dimension
- The datatype in the simulation domain, i.e. when the data is used by the federate, i.e. the input to the Normalization functions.
- The upper bound for any possible range when sent to the RTI. With NaturalGas being defined as [3..4) this means that 4 is the upper bound.
- The Normalization Function used to calculate the DDM Ranges from the simulation data. The input to the Normalization Function shall be based on the Datatype, as specified above. The output shall be in the range [0..Dimension Upper Bound). You may also refer to a function that is defined in some other document. Some commonly used functions, like linearEnumerated used above, are provided in Annex B of the IEEE 1516.2 standard.
- The default value to be used if no DDM information is provided. In a simple case like this we specify “Excluded”.

We have now specified the FuelTypeDim dimension. We also need to specify that this dimension can be used when updating or subscribing to the attributes of the Car object class. This has to be done for all attributes. Figure 7-6 shows how this is defined for the Name attribute.

![6-attribute-ddm.png](img%2F6-attribute-ddm.png)