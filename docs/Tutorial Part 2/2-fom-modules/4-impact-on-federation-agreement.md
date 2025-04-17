---
sidebar_position: 4
---

# Impact on the Federation Agreement

Note that it is not enough to split the FOM into modules. We also need to split the Federation Agreement into two parts. You may want to study Appendix A that describes the Federation Management module. It now contains the extended set of interactions.

In practice, you may work with federation agreements and FOM modules in two ways:

1.	In some cases you divide your FOM into several modules to split the work between different teams. The modules are meant to be used together. In this case you may want to write one federation agreement that covers several FOM modules.
2.	In other cases you want to create FOM modules that can be reused stand-alone, typically in a new, slightly different federation. In this case you should create a package of the FOM module and the corresponding federation agreement. 

When you reeuse the FOM module it will become a sub-federation agreement to the main federation agreement. Note that you may also be able to reuse parts of the program code or even libraries that implements support for the reusable FOM modules.
