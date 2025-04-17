---
sidebar_position: 3
---

# Monitoring the Federation

In every federation execution, the RTI will publish exactly one instance of the class HLAobjectRoot.HLAmanager.HLAfederation, which is also defined in the MIM module. By subscribing to this class and its attributes we can inspect some federation-wide information.

Here is an overview of the attributes of this class:

- General information, like federation name, time implementation and RTI version
- List of joined federates, or actually, handles of the federates
- Data related to the FOM modules in the federation
- Save/Restore related information
- Whether Auto provide is activated

To get a full description of all attributes, read the HLA standard and look at the MIM module. 
