---
sidebar_position: 5
---

# Creating a Region

Here is some sample code that shows how the publishing federate initially creates and commits the “Diesel” region.

The code does the following:
1.	Creates factories that we need.
2.	Gets a handle for the FuelTypeDim dimension
3.	Creates a set of Dimensions to be used.  It is stored in a DimensionHandleSet object. In this case we will only use one dimension, the FuelTypeDim.
4.	Create a new Region called DieselRegion that uses the dimensions in the above DimensionHandleSet.
5.	Create a RangeBounds object called dieselRangeBounds that specifies the range 1..2 (Diesel).
6.	Set the range for the FuelType dimension of the DieselRegion to this range.
7.	Since there may potentially be more regions, we need to put the single DieselRegion in a RegionHandleSet called dieselRegionHandleSet.
8.	Finally we commit the dieselRegionHandleSet. The new range will now take effect.

Some best practices are as follows:
a)	You may create the factories in step 1 initially in your federate and reuse it for both publication and subscription.
b)	Try to reuse the committed regions as much as possible. You can for example create one region for each type of fuel and then reuse it.

Here is the code:

```java
// 1. Get factories
DimensionHandleSetFactory myDimensionHandleSetFactory = rtiAmbassador.getDimensionHandleSetFactory();
RegionHandleSetFactory myRegionHandleSetFactory = rtiAmbassador.getRegionHandleSetFactory();

// 2. Get a handle for the FuelType Dimension
DimensionHandle fuelTypeDimHandle = rtiAmbassador.getDimensionHandle("FuelTypeDim");

// 3. Create a set of dimensions and add the FuelTypeDim
DimensionHandleSet myDimensions = myDimensionHandleSetFactory.create();
myDimensions.add(fuelTypeDimHandle);

// 4. Create a new (empty) Region with the FuelType Dimension. 
RegionHandle dieselRegion = rtiAmbassador.createRegion(myDimensions);

// 5. Set the lower and upper bound for the Diesel range 
long normalizedLowerBoundForDiesel = 1;
long normalizedUpperBoundForDiesel = normalizedLowerBoundForDiesel + 1;
RangeBounds dieselRangeBounds = new RangeBounds(normalizedLowerBoundForDiesel, normalizedUpperBoundForDiesel);

// 6. Set the range for the FuelType Dimension for the Diesel region
rtiAmbassador.setRangeBounds(dieselRegion, fuelTypeDimHandle, dieselRangeBounds);

// 7. Create a set of region (handles) and add the Diesel region
RegionHandleSet dieselRegionHandleSet = myRegionHandleSetFactory.create();
dieselRegionHandleSet.add(dieselRegion);

// 8. Finally commit the region set
rtiAmbassador.commitRegionModifications(dieselRegionHandleSet);

```