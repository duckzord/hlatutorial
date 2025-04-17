---
sidebar_position: 1
---

# Introduction 

When developing a federation, you use the FOM to specify the data types for attributes and parameters. HLA provides a rich set of predefined data types that you use as building blocks. The Object Model Template part of the standard, chapter x, specifies the data encodings in detail. 

When information is exchanged within a federation, each federate is responsible for encoding and decoding data according to the data types in the FOM. Incorrect encoding of data is one of the most common reasons for federations or federates to fail. The problem is caused by two factors:

1.	A sending federate encodes data incorrectly.
2.	A receiving federate assumes that the received data is correctly encoded

Both of these issues need to be properly addressed by federates. Even if your federate sends correctly encoded data it shouldn’t assume that the data received is correctly encoded.

The encoding helpers consist of a set of object classes that provide type-safe methods for converting local variables to and from byte-arrays, that can be used for exchanging data by the HLA services. There are some best-practices to be followed when using these classes:

1.	Keep the number of instantiated encoding helper objects to a minimum. Consider creating the objects initially and then reuse them.
2.	Use different object instances for encoding, when sending data, and decoding, when receiving data, since these classes are not thread-safe.
3.	Be sure to handle exceptions, in particular when receiving data. Log the exception and discard of any data that you don’t know is correctly decoded.
