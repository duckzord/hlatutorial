---
sidebar_position: 11
---

# Filtering on Position Using teh Dynamic Checkerboard DDM

We will now filter on the position of the car. As opposed to the fuel type the position, and the corresponding Region information, changes over time. We will call this method “dynamic DDM”. We will show two different approaches. The first one is informally called the checkerboard approach. In this case we have chosen to split the geographical area where the cars drive into 16 “checkerboard” squares. The car scenarios take place in be Bay Area of California within the Latitude degrees 121W and 123W and Longitude degrees 37N and 39N. Figure 7-12 shows the resulting map.

![11-checkboard-approach.png](img%2F11-checkboard-approach.png)

We number the 16 squares, numbered 0 to 15. In larger scenarios we may choose a larger number of squares, but sixteen will do for now. We call this dimension CheckeredPositionDim, since it is based on the position attribute. It uses a custom normalization function that we call Checkerboard. Figure 7-13 explains the dimension. 

![12-checkeredPositionDim-normalized.png](img%2F12-checkeredPositionDim-normalized.png)

To the left we can see PositionRec, the HLA datatype that the dimension is based upon. To the right we can see the range of normalized values. These are integers, starting with zero and up to, but not including 16. The value 16 is the Dimension Upper bound (DUB). In the middle we can see the normalization function that is used for converting data of the specified datatype to a normalized value. We locate the square in which the Latitude and Longitude values are located. Note that for a value of 38N, 121.1W, which is on the border between square 7 and 11 we must decide on a common strategy for which square to use, for example the lower numbered square.

Figure 7-14 shows the definition of the CheckeredPositionDim in the FOM: 

![13- checkeredPositionDim-normalized-FOM.png](img%2F13-%20checkeredPositionDim-normalized-FOM.png)

Throughout the execution we will use exactly these sixteen regions when sending updated. Since this is a fairly small number of regions we can create and save them initially. It is strongly recommended to reuse regions that you have created throughout the code, instead of creating additional, identical regions. 

In the previous case with fuel types, the region that a car uses never changed over time. In this case we want to change the association of all attributes of a car when it moves into a new square. This involves the following:

1.	Whenever the position of a car changes we need to check if it moved into a different square than before.
2.	If so, all attributes of the car should be associated with the new square instead of the old one. This is done by adding the new regions using the Associate Regions for Updates service. They also need to be unassociated with the previous region using the Unassociate Regions for Updates service. 

Here is a code example that shows how the association for the attributes of a car instance is changed from square five to square six.

```java
// 0. It is assumed that we already have region handles for _square5Region, _square6Region, etc

// 1. Get factories
RegionHandleSetFactory myRegionHandleSetFactory = _rtiAmbassador.getRegionHandleSetFactory();

// 2. Create region handle sets for square 5 and square 6
RegionHandleSet square5RegionSet = myRegionHandleSetFactory.create();
square5RegionSet.add(_square5Region);
RegionHandleSet square6RegionSet = myRegionHandleSetFactory.create();
square6RegionSet.add(_square6Region);

// 3. Create attribute handle set and get attribute handles as usual
// Not repeated

// 4. Create an association between the above set of attributes and the square 6 region
AttributeRegionAssociation carAttributesAndSquare6RegionAssociation = 
      new AttributeRegionAssociation(carAttributes, square6RegionSet);

// 5. Create a list of associations and add the Square 6 association
// We use a list that can potentially handle multiple pairs of attributes and regions
AttributeSetRegionSetPairList carAndSquare6PairList = myAttributeSetRegionSetPairListFactory.create(1);
carAndSquare6PairList.add(carAttributesAndSquare6RegionAssociation);

// 6. Associate the Car object instance with the above associations for Square 6
_rtiAmbassador.associateRegionsForUpdates(_carInstance, carAndSquare6PairList);

// 7. Create an association between the above set of attributes and the square 5 region
AttributeRegionAssociation carAttributesAndSquare5RegionAssociation = 
       new AttributeRegionAssociation(carAttributes, square5RegionSet);

// 8. Create a list of associations and add the Square 5 association
AttributeSetRegionSetPairList carAndSquare5PairList = myAttributeSetRegionSetPairListFactory.create(1);
carAndSquare5PairList.add(carAttributesAndSquare5RegionAssociation);

//9. Unassociate the Car object instance with the above associations
_rtiAmbassador.unassociateRegionsForUpdates(_carInstance, carAndSquare5PairList);

```