---
sidebar_position: 15
---

# Modifying the Regions

The major difference in this design pattern is that we modify the range of our regions. The following code example shows how to commit an update to the region that is associated with each car.

```java
// 1. Get factories and dimension handles
RegionHandleSetFactory myRegionHandleSetFactory = 
     _rtiAmbassador.getRegionHandleSetFactory();

DimensionHandle latitudeDim = _rtiAmbassador.getDimensionHandle("LatDim");
DimensionHandle longitudeDim = _rtiAmbassador.getDimensionHandle("LongDim");

// 2. Set the lower and upper bound for the latitude range
long normalizedLowerBoundForLat = 30;
long normalizedUpperBoundForLat = normalizedLowerBoundForLat + 4;
RangeBounds latRangeBounds = new RangeBounds(
         normalizedLowerBoundForLat, normalizedUpperBoundForLat);
_rtiAmbassador.setRangeBounds(_latLongRegion, latitudeDim, latRangeBounds);

// 3. Set the lower and upper bound for the longitude range
long normalizedLowerBoundForLong = 50;
long normalizedUpperBoundForLong = normalizedLowerBoundForLong + 6;
RangeBounds longRangeBounds = new RangeBounds(
         normalizedLowerBoundForLong, normalizedUpperBoundForLong);
_rtiAmbassador.setRangeBounds(_latLongRegion, longitudeDim, longRangeBounds);

// 4. Commit the region modifications
// We use a region handle set that can potentially handle multiple region handles
RegionHandleSet latLongRegionSet = myRegionHandleSetFactory.create();
latLongRegionSet.add(_latLongRegion);
_rtiAmbassador.commitRegionModifications(latLongRegionSet);
```

Note that committing an update to a region means that the overlap between subscribers and publishers may need to be recalculated, which consumes CPU cycles. If updates are frequently committed, performance will suffer. This may affect all federates that use DDM. If the region associated with the attribute updates can be made bigger, it will not need to be updated as frequently, but less filtering will take place.
