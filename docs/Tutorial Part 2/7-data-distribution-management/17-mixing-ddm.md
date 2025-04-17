---
sidebar_position: 17
---

# Mixing Federates that use and do not use DDM

When developing federations that need to handle large scenarios you may need to include federates that don’t use DDM, and that cannot be modified. This may negatively impact the scalability of the federation. There are two types of issues:

If a federate produces information, like car instances, that don’t have DDM information associated to the attributes, the RTI will associate something called the Default Region to them, which is [0 .. Dimension Upper Bound) for all Dimensions in the FOM. This matches all subscriptions, which means that nothing will be filtered out. The implication for a subscribing federate’s code is that it gets too much information. One workaround is to add some code in the subscribing federate, that disposes of the unwanted data.

If a subscribing federate doesn’t use DDM, it may become overloaded.
