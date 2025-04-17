---
sidebar_position: 4
---

# The Importance of Switches

From part 1 of the tutorial you may remember that the FOM contains a set of runtime switches in the Switches table. This module must be included in at least one module. We recommend to providing it in exactly one module. There are two good approaches for this:

1.	Provide it in one of the FOM modules that is specific to the simulation domain, in this case the Fuel Economy FOM Module. Avoid putting it in a generally reusable and domain neutral module like the Federation Management module.

2.	Put it in a separate module.

In this case we have chosen to put it in the Fuel Economy module since it will always be used in this federation.
