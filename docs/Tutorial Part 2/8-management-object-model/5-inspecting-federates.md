---
sidebar_position: 5
---

# Management Object Model Use Case: Inspecting Other Federates

As described in the introduction of this chapter, MOM is useful for getting more information about other federates in a federation.

- Subscribe to instances of HLAfederate to find out which other federates that exist in a federation. Then inspect the federate name, type and host of these federates.

- Use the HLAreportObjectClassPublications interaction, and related interactions for subscriptions and interactions, to understand what information other federates publish and subscribe to. Each call may result in many responses for each federate, one for each object or interaction class published or subscribed.

- There are also attributes that enables you to inspect the Time Management state of other federates, as described below.

- Get notified about any exceptions that are thrown when federates call RTI services. This is done by publishing the HLAsetExceptionReporting interaction and sending an interaction with the value of HLAreportingState to True for one or more federates. Any exception will then be reported by the RTI through an HLAreportException interaction.  Note that it is necessary to subscribe to that Interaction class.

- You may even inspect which HLA services another federate calls by HLAsetServiceReporting interaction. Note that enabling this reporting may result in a large number of HLAreportServiceInvocation callbacks, which in some cases may slow down the entire federation. Some RTIs provide local logging of callbacks, which may be a better choice in many federations.