---
sidebar_position: 5
---

# Configuring HLA Time Management in the FOM

We need to specify the logical time and how it should be interpreted in the FOM. The Time Representations is documented in the FOM as shown in Figure 6-5. In the Fuel Economy Federation we will use the standardized **HLAinteger64time** representing the number of microseconds from the start of the scenario. This enables us to simulate scenarios with a length of more than 292 471 years with very high accuracy. There is also another standardized time representation, **HLAfloat64time**, but we will use integer time since integer values are easier to inspect and verify. Note that we need to specify the time representation for both Timestamp and Lookahead, a concept we will describe later in this chapter. The Datatype used for these are usually the same.

![5-time-representation.png](img%2F5-time-representation.png)

We also need to verify that the attributes and interactions in the FOM use Timestamped Order (TSO) delivery, as opposed to Receive Order (RO). Figure 6-6 shows an attribute where TSO delivery has been selected.

![6-position-with-timestamp.png](img%2F6-position-with-timestamp.png)

Note that Timestamp Order delivery always uses the **HLAreliable** transportation. 

