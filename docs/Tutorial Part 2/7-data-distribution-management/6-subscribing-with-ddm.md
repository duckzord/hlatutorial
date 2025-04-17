---
sidebar_position: 6
---

# Subscribing with DDM

Here is some sample code that shows how the subscribing federate initially creates and commits the “Gasoline” and “Diesel” regions. Note that in this example we provide two different regions, one for Gasoline and one for Diesel. Note that steps 1-5 are identical with the above. 

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

// 4 (again). Create another (empty) Region with the FuelType Dimension 
RegionHandle gasolineRegion = rtiAmbassador.createRegion(myDimensions);

// 5 (again). Set the lower and upper bound for the Gasoline range 
long normalizedLowerBoundForGasoline = 0;
long normalizedUpperBoundForGasoline = normalizedLowerBoundForGasoline + 1;
RangeBounds gasolineRangeBounds = new RangeBounds(normalizedLowerBoundForGasoline, normalizedUpperBoundForGasoline);

// 6 (again). Set the range for the FuelType Dimension for the Gasoline region
rtiAmbassador.setRangeBounds(gasolineRegion, fuelTypeDimHandle, gasolineRangeBounds);

// 7. Create a set of region (handles) and add the Diesel and Gasoline regions
RegionHandleSet gasolineAndDieselRegionHandleSet = myRegionHandleSetFactory.create();
gasolineAndDieselRegionHandleSet.add(dieselRegion);
gasolineAndDieselRegionHandleSet.add(gasolineRegion);

// 8. Finally commit the region set
rtiAmbassador.commitRegionModifications(myRegionHandleSet);

// 9. Finally subscribe to car attributes in these two regions
TBD: Subscribe Name, LicensePlateNumber, FuelType, FuelLevel, Position with above RegionHandleSet

```