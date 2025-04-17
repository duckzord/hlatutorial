---
sidebar_position: 10
---

# Troubleshooting a Time Managed Federation

If Time Management doesn’t behave as expected in your federation there are several ways to find the problem. Here are some things you should check:

**Do all federates interpret the Logical Time in the same way?**
If one federate interprets the 64 bits as an integer and the rest as a float the result will be unexpected and incorrect. If you suspect that you have a problem here you may need to check with developers, documentation or even the code. Note that some general-purpose tools have configurable time representation.

**Is regulating/constrained set up correctly in the federation?**
This can usually be inspected in the user interface of the RTI. 

**Has the federation stopped completely?**
This usually depends on one federate not advancing time. Check in the user interface of the RTI which federates that are not in the advancing state. Check which of the federates that has the lower GALT (described later). Try resigning these federate using the user interface of the RTI.

**Does logical time move too slowly?**
This may depend on the pacer federate not running fast enough or some federate not completing calculations within the given time frame. First try to run the pacer federate alone. Then try to find the straggler, i.e. the federate that is the last federate to do a time advance request. In some cases the scenario may be too big or a computer too slow to meet the deadline.
