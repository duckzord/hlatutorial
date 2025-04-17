---
sidebar_position: 14
---

# Filtering on Position Using the Dynamic Floating DDM

We will now show another way to filter on the position of the car that we will call Dynamic Floating DDM. In this case we will not use a predefined set of DDM regions as in the two previous examples. Instead we will have one region per car, that moves around with the car. We will use one dimension for latitude and one for longitude. For LatitudeDim we will split up the 121W to 123W into 100 pieces. Similarly, for LongitudeDim we will split up the 37N to 39 N into 100 pieces.

We will also create one region for each car object instance. As the car moves we will modify the region to match, making it “float” around as opposed to the fixed grids used earlier. This is shown in figure 7-16. Since the DDM regions of the cars are updated over time we informally call it dynamic floating DDM. The following picture shows the dimensions, the regions for two cars and one subscribing MapViewer federate.

![15-floating-region-overlap.png](img%2F15-floating-region-overlap.png)

Figure 7-17 below illustrates the normalization function.

![16-floating-normalization-fueltypedim.png](img%2F16-floating-normalization-fueltypedim.png)

In this case we use two dimensions, one for latitude, called LatitudeDim, and one for longitude, called LongitudeDim. They both work the same way so let’s look at the normalization for the LatitudeDim.

To the left we can see AngleFloat64, the HLA datatype that the dimension is based upon. To the right we can see the range of normalized values. These are integers, starting with zero and up to, but not including 100. The value 100 is called the Dimension Upper bound (DUB). In the middle we can see the normalization function that is used for converting data of the specified datatype to a normalized value. In this case we map the range of floating point values 121.0 to 123.0 to the integer value 0 to 99.
