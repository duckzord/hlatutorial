---
sidebar_position: 2
---

# Principles for building data types

Wherever we define an attribute or a parameter you need to provide a data type. In part 1 of the tutorial we have shown examples of how to define data types. Now it is time to take a closer look at the principles that can be used.

**Simple data types**
These are typically used for describing integer, float and Boolean values. When you specify a simple data type, you need to provide a representation. This representation is described using a Basic Datatype.

![simple_datatype.png](img%2Fsimple_datatype.png)

**Enumerated Datatype**
These are used to describe enumerated values. The representation must have discrete values. We recommend using a 32 bit integer.

![enumerated_datatype.png](img%2Fenumerated_datatype.png)

A list of enumerators (strings) and the corresponding values (numbers) must be provided. Make sure that the numbers can be represented using the chosen representation.

**Array Datatypes**
This datatype can be used to create dynamic or fixed size arrays of more or less anything. Two of the predefined datatypes, HLAASCIIstring and HLAunicodeString are examples of array datatypes. 

![array_dataype.png](img%2Farray_dataype.png)

Note that the array consists of elements like simple data types, enumerated data types, fixed records, variant records or even arrays. The cardinality can be specified as the keyword “Dynamic” or an integer value. It is also possible to specify multidimensional arrays.

For encoding, use the keyword “HLAvariableArray” for dynamic arrays and “HLAfixedArray” when a fixed number of elements was specified. The HLAvariableArray encoding uses an HLAinteger32BE to store the number of elements. 

**Fixed Record Datatypes**
This datatype is used to create records, consisting of elements of other datatypes. A typical use case is a position where it doesn’t make sense to send the most recent value for latitude without sending the longitude. 

![fixed_record_datatype.png](img%2Ffixed_record_datatype.png)

Any number of fields can be specified. Just like arrays the type of each field can be simple data types, enumerated data types, fixed records, variant records or arrays. For encoding use the “HLAfixedRecord” keyword.

There is also a VariantRecord datatype that can be used to specify different sets of fields for different variants. A special field, called the discriminant, is used to determine which set of fields that shall be used in each case.



