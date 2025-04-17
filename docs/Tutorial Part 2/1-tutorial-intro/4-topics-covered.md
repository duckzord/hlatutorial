---
sidebar_position: 4
---

# Topics Covered

The chapters of this part of the HLA Tutorial are as follows:

**FOM Modules**
This chapter shows why and how to decompose a growing FOM into modules. It also discusses how to generalize FOMs for reuse.  
**Data types**
This chapter shows how to define HLA data types from simple data types to more complex types.  
**Synchronization Points**
This chapter shows how to synchronize a federation using synchronization points.  
**Ownership Management**
This chapter shows how to transfer the ownership of an attribute from one federate to another  
**Time Management**
This chapter shows how to manage time across a federation to ensure causality and consistency  
**Filtering and Data Distribution Management**
This chapter shows how to limit the data flow by filtering on user-defined dimensions  
**The Management Object Model**
This chapter shows how you can inspect and control the state of the federation using management objects and interactions.  
**More HLA Features**
This chapter describes some additional HLA features.  
**More on Encoding Helpers**
This chapter shows how to correctly encode and decode more complex data structures using the Encoding Helpers  
**Federate and federation performance**
This chapter describe how to plan, implement and verify optimal performance in your federation  
**Fault Tolerance**
This chapter describes how to design and implement fault tolerance in your federation  
**The Levels of Conceptual Interoperability**
This chapter revisits the concept of Interoperability, which is the overall purpose of HLA. It provides a model for different levels of interoperability. It also provides checklists of how different levels are achieved using HLA and other means.  

In addition to this there are two appendices:  
**Appendix A: Federation Agreement**
Here a complete federation agreement, using all the above HLA features, is provided.  
**Appendix B: Federation Object Model**
This is the set of FOM Modules for the federation.

### The Standards documents

The HLA standard consists of three parts:

1. The “Rules” (IEEE 1516-2010) that contains ten rules for the federates and the federation
2. The “Interface Specification” (IEEE 1516.1-2010) that describes the RTI services in detail
3. The “Object Model Template” (IEEE 1516.2-2010) that describes the format for FOMs.
The purpose of the standard is to give a full and exact specification of the High-Level Architecture whereas this document explains the standard and how to use it without providing every detail.

You should consider getting a copy of these standards. In particular the Interface Specification is strongly recommended when developing federates. The recommended way to get these standards is to become a SISO member since this gives you access to all IEEE standards developed by SISO. You may also visit the IEEE web site and buy them.

### A summary of the HLA Rules
HLA provides ten rules for federates and federation in the standards document “HLA Rules”. Here is a simplified version of these rules. The rules use the concept of a Simulation Object Model, SOM. The SOM is very similar to a FOM. It is based on the same format, the HLA object model template. It describes what information one particular federate can publish and subscribe.

Note that the FOM relates to one particular federation. A SOM relates to what a federate can publish and subscribe in any potential federation. You may think of it as a brochure advertising the capabilities of a federate. In a particular federation the federate may only publish and subscribe to a subset of the object and interaction classes in the SOM.

#### Federation rules
1. All federations shall have a FOM
2. The federates shall store the attribute values, not the RTI
3. For the information that is described in the FOM, all data exchange shall be performed using the RTI
4. Federates shall only interact with the RTI using the services described in the interface specification
5. Each attribute of any object instance may only have one federate that owns is (and is thus allowed to update it) at any given time

#### Federate rules
6. Federates shall have a SOM
7. Federates shall send and receive data according to their SOM
8. Federates shall be able to transfer ownership according to their SOM
9. Federates shall follow their FOM with regards to how they send/receive attribute updates
10. Federates shall manage their internal time in such a way that it can be coordinated with the data exchange with other federates using HLA services