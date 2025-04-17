---
sidebar_position: 2
---

# Sample Datatypes used in this Chapter

This chapter provides examples in C++ and Java for a number of data types. The examples are related to the Fuel Economy federation, although they are extensions to the original FOM. Detailed examples of how to encode and decode all the datatypes introduced here can be found in the Java Encoding Helpers or C++ Encoding Helpers sections below.

#### Simple Datatype
The OctaneRatingInt32 is a simple datatype used to specify the octane rating of gasoline. All simple datatypes has a basic datatype representation, in this case HLAinteger32BE.

![1-OctaneRatingInt32.png](img%2F1-OctaneRatingInt32.png)

#### Enumerated Datatype
An enumerated datatype also has a basic datatype representation which makes working with encoding/decoding of simple datatypes and enumerated datatypes very similar. Below is the definition of DieselEnum32.

![2-DieselEnum32.png](img%2F2-DieselEnum32.png)

#### Fixed Array Datatype

A fixed array will have a fixed number of elements. The elements themselves can be any of the datatypes available in HLA. In the LeaderBoard fixed array below the element type is HLAunicodeString which itself is a variant array. It is possible to build up very complex data structures by nesting datatypes like this.

![3-LeaderBoardArray.png](img%2F3-LeaderBoardArray.png)

#### Variable Array Datatype

The difference between a fixed array and a variable array is that the variable array can vary in size. Below is the definition of CarNameArray which will contain all the names of the cars currently in the federation, the size of the array will change as cars are created and deleted.

![4-CarNameArray.png](img%2F4-CarNameArray.png)

#### Fixed Record Datatype

A fixed record will have a fixed number of fields and each field has its own datatype (as opposed to an array in which all elements are of the same datatype). The GasolineRec fixed record below has two fields with different datatypes, OctaneRatingInt32 and HLAboolean.

![5-GasolineRec.png](img%2F5-GasolineRec.png)


#### Variant Record Datatype

The variant record is the most complex datatype to work with. A variant record will have a discriminant which will always be of an enumerated datatype and a set of alternatives. Each alternative has its own datatype, similar to a field in a fixed record. The value of the discriminant will specify which of the alternatives are currently used. It is only the alternative specified by the discriminant that will actually be encoded and sent over the network.

In the FuelStatusVariantRec datatype below the discriminant is the type FuelTypeEnum32. If the value of the discriminant is Gasoline, the content of the variant record is a GasolineRec fixed record (as described above), but if the value of the discriminant is Diesel then the content would be a DieselRec fixed record.

![6-FuelStatusVariantRec.png](img%2F6-FuelStatusVariantRec.png)


