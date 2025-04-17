---
sidebar_position: 8
---

# Changing the Subscription

In the FuelDimension case, the type of fuel for a specific car will probably not change during a federation execution. It is more likely that a MapViewer, used for inspecting a scenario, will change subscriptions when an operator wants to inspect the progress of cars with different fuel types. The MapViewer will then dynamically change the subscribed regions for the Car object class.

In order to subscribe to more regions, for example Ethanol cars, you simply perform one more subscription for the car class with this additional region.

To remove the Diesel region subscription, you make an Unsubscribe Object Class Attributes With Regions with the Diesel region. This will subtract the Diesel region from the subscription, but the Gasoline region subscription remains.

When changing a subscription, it is recommended that you first subscribe to the new region and then unsubscribe to the previous region. Doing it in this order will give convenient Scope notifications. The concept of Scope is described in the next section.

```java
// 1. Get class and attribute handles as above.
// Not repeated here

// 2. Get factories
RegionHandleSetFactory myRegionHandleSetFactory = _rtiAmbassador.getRegionHandleSetFactory();

// 3. Create a set of region (handles) and add the Ethanol region
RegionHandleSet ethanolRegionHandleSet = myRegionHandleSetFactory.create();
ethanolRegionHandleSet.add(_ethanolRegion);

// 4. Build attribute and region association and subscribe
AttributeSetRegionSetPairList attributesAndEthanolRegions =   
  _rtiAmbassador.getAttributeSetRegionSetPairListFactory().create(1);
attributesAndEthanolRegions.add(new AttributeRegionAssociation(carAttributes,   
   ethanolRegionHandleSet));

_rtiAmbassador.subscribeObjectClassAttributesWithRegions(carClassHandle, attributesAndEthanolRegions);

// 5. Create a set of region (handles) and add the Diesel region
RegionHandleSet dieselRegionHandleSet = myRegionHandleSetFactory.create();
      dieselRegionHandleSet.add(_dieselRegion);

// 6. Build attribute and region association and unsubscribe
AttributeSetRegionSetPairList attributesAndDieselRegion = _rtiAmbassador.getAttributeSetRegionSetPairListFactory().create(1);
attributesAndDieselRegion.add(new AttributeRegionAssociation(carAttributes, dieselRegionHandleSet));

_rtiAmbassador.unsubscribeObjectClassAttributesWithRegions(carClassHandle, attributesAndDieselRegion);
```