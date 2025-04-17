---
sidebar_position: 6
---

# Management Object Module Use Case: Inspecting the FOM

A generic management federate or a data logging federate may be interested in the FOM that is used in the federation. As many federates can join and add more FOM modules, the resulting FOM may not be known by all federate developers in advance.

- The attribute HLAFOMmoduleDesignatorList of the HLAfederation object class provides the list of the designators of the currently loaded FOM modules.

- Once you have retrieved the designators for the FOM modules, you may request their XML content using the HLArequestFOMmoduleData. Use an XML parser, and the HLA DIF XML Schema, to parse and investigate the content.

- You may also check, for each federate, which FOM modules they have provided.