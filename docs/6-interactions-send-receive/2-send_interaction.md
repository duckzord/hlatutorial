---
sidebar_position: 2
---

# Sending Interactions

To send an interaction, we will encode the parameter values and send the interaction. In this example the destination will be San Jose and the initial fuel amount will be 40 liters. Here is the pseudo code:

```cpp
myStringEncoder.setValue(“San Jose”)
myInt32BEencoder.setValue(40)

parameters[destinationParameterHandle] = myStringEncoder.encode()
parameters[initialFuelAmountParameterHandle] = myInt32BEencoder.encode()

rti.sendInteraction(scenarioInteractionHandle, parameters, userSuppliedTag)
```

Note that we use the encoders that we created earlier and assign the desired values, i.e. San Jose and 40. This is done with the “=“ operator in C++ and “setValue” in Java. We then build the parameter structure which is a map consisting of pairs of parameter handles and encoded values. By calling the encode method for an encoder we will get a correctly encoded byte array, no matter how complex the data to be encoded is. It may be slightly overkill to use encoding helpers for an integer but this will guarantee that the encoded result is correct.

When we send the interaction we can also provide a user supplied tag. In this case it is empty.

### HLA Service: Send Interaction
This service sends an interaction and the supplied parameter values. A user supplied tag can be provided.

Read more about Send Interaction in section 6.12 of the HLA Interface Specification.