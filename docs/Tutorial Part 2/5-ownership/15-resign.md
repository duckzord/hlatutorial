---
sidebar_position: 15
---

# Resign and Ownership Management

In the HLA Tutorial part one the Resign services was introduced. As part of the resign there is a Resign Directive that tells the RTI what to do with respect to ownership when that federate resigns. The recommended resign directive for most federations is CANCEL_THEN_DELETE_THEN_DIVEST. This means that the RTI will do the following actions when the federate resigns, in the following order:

1.	Cancel all ongoing attempts to acquire ownership
2.	Delete all the object instances for which the federate owns the HLAprivilegeToDeleteObject attribute
3.	Divest all attributes that it still owns, after the object deletions caused by the previous step.

There are additional resign directives, as described in the standard. You may for example want to avoid deleting object instances in a federation where there are other federates standing by to take over ownership.
