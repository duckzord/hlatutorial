---
sidebar_position: 16
---

# Push Ownership Transfer

So far we have only covered “pull” ownership transfer since this is easier to manage when you implement your first federation. There are a three main “push” ownership transfer mechanisms that a federate can initiate:

**Attribute Ownership Divestiture If Wanted**, whereby a federate will divest attributes only if there is some other federate that is standing by to acquire ownership of these attributes. Otherwise no divestiture will take place. 

**Negotiated Attribute Ownership Divestiture**, whereby a federate will try to divest attributes. If another federate is already standing by to acquire ownership of the attributes, the ownership may be transferred, if the divesting federate confirms this. This may also result in the RTI trying to find a federate, which is not currently acquiring, that can acquire these attributes, which must also be confirmed by the acquiring federate. It may also result in the request to remain pending until the divesting federate cancels the request.

**Unconditional Attribute Ownership Divestiture**, whereby a federate can divest (make unowned) attributes without further negotiation. This may or may not result in another federate taking ownership of them.

An important callback that is related to the two later divestiture services is:

**Request Attribute Ownership Assumption** (callback) that informs a federate that it can acquire ownership of certain attributes. This callback may be received by a federate that publishes these attributes even if it is not actively trying to acquire ownership of these attributes. It is particularly interesting when triggered as a result of a Negotiated Attribute Ownership Divestiture call or as a result of another federate resigning or crashing.

Read more in the HLA interface specification about these services.
