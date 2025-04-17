---
sidebar_position: 6
---

# Setting up HLA Time Management in the CarSim Federates

We will now look at some sample code that implements time management. The first place we encounter time is in the Create Federation Execution call.

```java
rti = RTIambassadorFactory.createRTIambassador()
rti.createFederationExecution(“MyFederation”, “MyFOM”, “”, “HLAinteger64time”)
```

The RTI needs to know what time representation that will be used in the federation since it needs to compare timestamps. It is highly recommended that you use one of the two standard time representations, HLAinteger64time or HLAfloat64time, although advanced users can implement their own representations.

We also need to create our own variable to represent our logical time. Note that time is a C++ or Java object that we need to create. In this example we create a time object with the time 0 (zero). 

In order to specify our time steps we also need to create a time interval. In this example we create a time interval object with the interval 1.

```java
HLAinteger64TimeFactory timeFactory = (HLAinteger64TimeFactory)_rtiAmbassador.getTimeFactory();
HLAinteger64Time _tCurrent = timeFactory.makeTime(0);
HLAinteger64Interval _step = timeFactory.makeInterval(1);
```

We also need to tell the RTI, just after joining the federation, that we will receive timestamped messages. We will be affected by other federates so in HLA our federate will be considered Time Constrained. In this case we check if we have become Time Constrained every 10 ms.

```java
_constrained = false;
    _rtiAmbassador.enableTimeConstrained();
    while (!_constrained) {
       // Wait for callback
		Thread.sleep(10);
    }
```

The RTI will then send a callback telling us that the federate is now Time Constrained. The RTI will provide a time value, which will be zero if no other federate has started advancing time. 

 ``` java
void timeConstrainedEnabled(LogicalTime t)  //Callback
{
    _tCurrent = (HLAinteger64Time)t;
    _constrained = true;
}
```

In the same way we need to tell the RTI, just after joining the federation, that we will send timestamped messages. This will affect other federates so in HLA our federate will be considered Time Regulating. We also need to tell the RTI the Lookahead, which in this case is the length of our time step. Lookahead is discussed in detail later in this chapter.

``` java
_rtiAmbassador.enableTimeRegulation(new LogicalTimeLookaheadLong(1));
 	while (!_regulating) {
       	// Wait for callback
			Thread.sleep(10);
 	}
```

The RTI will then send a callback telling us that the federate is now Time Regulating. The RTI will provide a time value, which will be zero if no other federate has started advancing time.. 

``` java
//Callback
void timeRegulationEnabled(LogicalTime t)
{
       _tCurrent = (HLAinteger64Time)t;
       _regulating = true;
}
```

It is recommended that you enable Time Constrained and Time Regulating in the above order and that you do this before you publish or subscribe or start advancing time.
