---
sidebar_position: 7
---

# Sending Updates with DDM

We now have the DDM regions in place. Let’s have a look at the code used in the Car simulators. Here is some sample code that shows how the publishing federate registers a car. The registration associates the “Diesel” region with the attribute Name, LicensePlateNumber, FuelType, FuelLevel and Position of the car instance.

```java
// 1. Create factories
AttributeHandleSetFactory myAttributeHandleSetFactory = rtiAmbassador1.getAttributeHandleSetFactory();
AttributeSetRegionSetPairListFactory myAttributeSetRegionSetPairListFactory = rtiAmbassador1.getAttributeSetRegionSetPairListFactory();

// 2. Create a set of attributes and add the Car attributes (using handles)
AttributeHandleSet attributeSetName = myAttributeHandleSetFactory().create();
attributeSetName.add(attributeName);
attributeSetName.add(attributeLicensePlateNumber);
attributeSetName.add(attributeFuelType); 
attributeSetName.add(attributeFuelLevel);
attributeSetName.add(attributePosition);

// 3. Create an association between the above set of attributes and the Diesel region
AttributeRegionAssociation carAttributesAndDieselRegionAssociation = new AttributeRegionAssociation(attributeSetName, dieselRegionHandleSet);

// 4. Create a list of associations and add the above association
AttributeSetRegionSetPairList myAttributeSetRegionSetPairList = myAttributeSetRegionSetPairListFactory.create(1);
myAttributeSetRegionSetPairList.add(carAttributesAndDieselRegionAssociation);

// 5. Register a Car object instance with the above associations
ObjectInstanceHandle carInstance = rtiAmbassador.registerObjectInstanceWithRegions(clsCar, myAttributeSetRegionSetPairList);
```

The federate can now send updates that will automatically use the associated regions. This code is identical to the non-DDM code.

```java
// 6. Send attribute update
rtiAmbassador.updateAttributeValues(carInstance, attributeHandleValueMap, userSuppliedTag)


Let us now look at the subscribing federate, in this example the MapViewer. This is the code for subscribing to diesel cars


// 1. Get factory for Region Handle Set
RegionHandleSetFactory myRegionHandleSetFactory = _rtiAmbassador.getRegionHandleSetFactory();

// 2. Create a set of region (handles) and add the Diesel region
RegionHandleSet dieselRegionHandleSet = myRegionHandleSetFactory.create();
dieselRegionHandleSet.add(_dieselRegion);

// 3. Get car class handle and the attribute handles
ObjectClassHandle carClassHandle = _rtiAmbassador.getObjectClassHandle("Car");
AttributeHandle carNameAttribute = _rtiAmbassador.getAttributeHandle(carClassHandle, "Name");
AttributeHandle carLicensePlateNumberAttribute = _rtiAmbassador.getAttributeHandle(
         carClassHandle, "LicensePlateNumber");
AttributeHandle carFuelTypeAttribute = _rtiAmbassador.getAttributeHandle(carClassHandle, "FuelType");
AttributeHandle carFuelLevelAttribute = _rtiAmbassador.getAttributeHandle(carClassHandle, "FuelLevel");
AttributeHandle carPositionAttribute = _rtiAmbassador.getAttributeHandle(carClassHandle, "Position");

// 4. Create handle set factory and populate with attribute handles
AttributeHandleSet carAttributes = _rtiAmbassador.getAttributeHandleSetFactory().create();
carAttributes.add(carNameAttribute);
carAttributes.add(carLicensePlateNumberAttribute);
carAttributes.add(carFuelTypeAttribute);
carAttributes.add(carFuelLevelAttribute);
carAttributes.add(carPositionAttribute);

// 5. Build attribute and region associations
AttributeSetRegionSetPairList attributesAndRegions = _rtiAmbassador.getAttributeSetRegionSetPairListFactory().create(1);
attributesAndRegions.add(new AttributeRegionAssociation(carAttributes, dieselRegionHandleSet));

// 6. Subscribe using the attributes and associations
_rtiAmbassador.subscribeObjectClassAttributesWithRegions(carClassHandle, attributesAndRegions);
```
The subscribing federate will now start discovering diesel cars and get attribute updates. If you want to include gasoline cars, you can simply perform a similar subscription for gasoline cars. Since HLA subscriptions are additive, the subscribing federate will now start discovering gasoline cars. 

