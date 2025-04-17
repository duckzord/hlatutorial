---
sidebar_position: 1
---

# Overview of HLA Services

Let’s have a closer look at the MIM. The three most important parts of the MIM are:

- The HLAobjectRoot and HLAinteractionRoot that are the starting point for building a hierarchy of object and interaction classes
- A number of predefined data types that are commonly used. These will be described in this section.
- The Management Object Model (MOM) which enables us to inspect and control the federation. This will be described in a later chapter.

The predefined data types in the MIM are as follows:

A number of Basic Data Types that can be used to describe the representation of your own Simple Data Types, Enumerated data types and a few more things. 
These are:

|Integers|Floats| General Binary |
|---|---|----------------|
|HLAinteger16BE|HLAfloat32BE|HLAoctet|       
|HLAinteger16LE|HLAfloat32LE|HLAoctetPairBE|
|HLAinteger32BE|HLAfloat64BE|HLAoctetPairLE|
|HLAinteger32LE|HLAfloat64LE||
|HLAinteger64BE|||
|HLAinteger64LE||||
		

The “16BE” at the end of, for example, an integer data type indicates that it is a 16 bit integer that is transmitted with a Big Endian byte ordering. This tutorial uses Big Endian everywhere since it is commonly used in the HLA community. For integers it makes sense to use no smaller than 32 bit representations considering how the CPUs of today move data. For floating point values you need to understand the resolution needed by your application. In our federation a 32 bit float is not sufficient for describing the position of a car using latitude and longitude so a 64 bit float was chosen.

Some other important predefined simple data types, that can be used directly for example for attributes and parameters are:

|Characters|Strings|General|Time Representations|
|---|---|---|---|
|HLAASCIIchar|HLAASCIIstring|HLAboolean|HLAinteger64time|
|HLAunicodeChar|HLAunicodeString|HLAbyte|HLAfloat64time

We recommend using Unicode strings rather than ASCII. The two time representations will be covered in the section about time management. As you have noticed everything in the FOM is prefixed with the letters “HLA” since it is part of the HLA standard. Your own classes and data types shall not use the “HLA” prefix.


