---
sidebar_position: 4
---

# MOM Interactions - General

MOM provides many interaction classes that can be used to request additional data. These relate to the entire federation or to a particular federate. There are three basic types of interactions:

- Request/Report interactions. A federate sends a request and the RTI replies with a corresponding response interaction. One example is to request the current subscriptions of a particular federate.

- Adjust. A federate sends an adjust interactions to adjust some state of the federation. One example is to change the ownership status of an attribute of an object instance.

- Service. A federate sends a service interaction that invokes an HLA service on behalf of another federate. One example is to perform an unsubscribe of an attribute on behalf of another federate. These interactions may create difficulties in a federation, since a federate will assume one state, but another federate has silently changed that state. Unless you are an advanced HLA developer you are recommended to avoid using these interactions.

If a MOM interaction that your federate sends results in an exception, this will result in the RTI sending an HLAreportMOMexception interaction. Remember to subscribe to this interaction class, if you intend to use MOM interactions.

MOM interactions also use two particular DDM dimensions:

- HLAfederate. This dimension can be used to filter attribute updates for instances of the HLAfederate object class. It can also be used to filter HLAreport interactions.
 
To create a region for this dimension, you need to start by fetching the federate handle, for example from an HLAfederate instance, and call the NormalizeFederateHandle service. The normalized federate handle is also used as a parameter for all interactions that your federate sends, that relate to a particular federate.

- HLAserviceGroup. This dimension is only used for ServiceReporting (see below). It enables you to filter on which service group that the interaction relates to. Regions for this dimension are based on the HLAnormalizedServiceGroup enumerated data type.

In this context, it is also worth mentioning a slightly related RTI service: List Federation Executions, which makes it possible to find out which federation executions that are available. This service can be called before joining a federation execution, as opposed to the MOM services, that are only available when joined to a federation execution. 
