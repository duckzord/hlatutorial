---
sidebar_position: 4
---

# HLA as a standard

### Open Standards

HLA is an open international standard, developed by the Simulation Interoperability Standards Organization (SISO) and published by IEEE. The development process is open and transparent. Everyone can participate in the development, suggest improvements, take part in the discussions and vote.

HLA is a standards document that describes the components of HLA and what interfaces and properties they must have. Anyone can develop any software component of HLA. Implementations of the different components are today available from commercial companies, governments, academia, and open source developers.

HLA is today a prescribed or recommended standard, for example in NATO as well as by national departments of defense. By establishing such policies, it is possible to facilitate the interoperability of different systems that are acquired over time by an organization.

Another effect of standards is that they enable a marketplace. When systems from different suppliers become interoperable, an end user can select and combine systems that meet his requirements. This reduces the cost, time, and risk for the end user while providing more opportunities for system vendors.

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