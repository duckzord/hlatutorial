---
sidebar_position: 13
---

# Unowned Attributes

What happens to the ownership of attributes when a federate that owns them disappears, typically because it crashed or resigned? The attribute will in this case become unowned. This means that there is no federate that can update it. These attributes are still monitored by the RTI. Ownership can thus be offered to other federates, making it possible to continue the simulation of these attributes. This is a key building block for fault tolerant federations, as described in a later chapter.   