---
sidebar_position: 8
---

# Management Object Module Use Case: Time Management

If you want to get an insight into how logical time is managed in the federation and in each federate, you can use MOM.

•	The object class HLAfederation contains the attribute HLAtimeImplementationName, which tells you which time implementation that is used. This can be useful when interpreting logical time values.

•	The object class HLAfederate has several attributes, for example the HLAfederateState, which tells you whether the federate is in the advancing or granted state, the HLAlogicaltime, which gives the time to which the federate has been granted, the HLAlookahead, which gives the lookahead as well as GALT and LITS (read the standard for details).
