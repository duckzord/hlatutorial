---
sidebar_position: 3
---

# Receiving Interactions

The RTI will deliver interactions to our federate by making calls to our Federate Ambassador, also known as a callback. This is the first time that we show a callback in this tutorial. There is a predefined Federate Ambassador called the NullFederateAmbassador with no functionality. It is recommended that you subclass the NullFederateAmbassador and then override selected methods. In this way your federate will support all callbacks even if you haven’t provided any code for all callbacks.

To handle an incoming interaction we need to decide which type of interaction this is and then decode its parameters. We recommend using separate encoding helper objects for calls and callbacks. Here is some pseudocode:

```cpp
Method FederateAmbassador.ReceiveInteraction(theInteraction, theParameterValues, TheUserSuppliedTag)

IF theInteraction=scenarioInteractionHandle THEN
    myStringEncoder.decode(theParameterValues[destinationParameterHandle])
    wstring ws = myStringEncoder
    myInt32BEencoder.decode(theParameterValues [initialFuelAmountParameterHandle])
    int fuel = myInt32BEencoder.getValue()
END IF
```

First we check which type of interaction this is. If it is the LoadScenario interaction then we can fetch the parameter values. We pass them to the decode method of the encoders. This code assumes that we always get both parameters. A safer approach is to loop through the parameters to check which parameters that are present. Note that the decoders may also throw exceptions if the incoming data is incorrect.

### HLA Service: Receive Interaction (callback)
In this example we have simplified the parameter list. There are also optional parameters like a time stamp. Note also that there are actually three different versions of the ReceiveInteraction method for the FederateAmbassador in the APIs. Different versions will be called depending on how many optional parameters that are present. It is highly recommended that you dispatch the calls that you don’t use, in this case the ones with additional optional parameters, to the version of the service that you have actually implemented.

Read more about Receive Interaction in section 6.13 of the HLA Interface Specification.