---
sidebar_position: 12
---

# The HLA Time Management Services

### HLA Service: Enable Time Constrained
This service is called to request that the federate wants to be time constrained, i.e. it receives timestamped messages. Note that the federate will not actually be constrained until it has received the corresponding callback. This callback will also contain a logical time to which the federate is granted. If no federate has started advancing time this will be zero. 

Read more about Enable Time Constrained in section 8.5 in the Interface Specification

###HLA Service: Enable Time Regulating 
This service is called to request that the federate wants to be time regulating, i.e. it sends timestamped messages. Note that the federate will not actually be regulating until it has received the corresponding callback. This callback will also contain a logical time to which the federate is granted. If no federate has started advancing time this will be zero.

Read more about Enable Time Regulating in section 8.2 in the Interface Specification

### HLA Service: Time Advance Request
This service is called to request that the federate be granted to a new, requested, logical time. The federate also promises that it will not send any timestamped messages with timestamp less than the requested time plus Lookahead. 

Read more about Time Advance Request in section 8.8 in the Interface Specification

### HLA Service: Time Advance Grant (callback)
This callback is delivered from the RTI to inform the federate that it has now been advanced to the logical time provided in the callback. The federate may not send any timestamped messages with timestamp less than the granted time plus the Lookahead. Note that in simple cases, like our CarSim federation, the federate will be granted to the requested time, but there exists more advanced cases where the federate may be advanced to a smaller logical time. 

Read more about Time Advance Grant in section 8.13 in the Interface Specification

### HLA Service: Enable Time Constrained
This service is called to request that the federate wants to be time constrained, i.e. it receives timestamped messages. Note that the will not actually be constrained until it has received the corresponding callback. This callback will also contain a logical time to which the federate is granted. If no federate has started advancing time this will be zero. If some federates has started advancing time, it will be granted to a logical time big enough so that the federate will not get a message in the past. It is up to the federate to decide if this is acceptable to its current scenario and simulation models.

Read more about Enable Time Constrained in section 8.5 in the Interface Specification

### HLA Service: Enable Time Regulating 
This service is called to request that the federate wants to be time regulating, i.e. it sends timestamped messages. Note that the will not actually be regulating until it has received the corresponding callback. This callback will also contain a logical time to which the federate is granted. If no federate has started advancing time this will be zero. If some federates has started advancing time, it will be granted to the smallest logical time that the federate can use for producing messages, given its Lookahead. This logical time may sometimes seem odd. Example: If your federate has a Lookahead/time step of 100 and the GALT is 800 then your federate would be granted to 701. In many cases you may then want to advance to the nearest, sensible logical time for you federate, in this case 800 before starting to simulate.

Read more about Enable Time Regulating in section 8.2 in the Interface Specification

