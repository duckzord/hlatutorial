---
sidebar_position: 5
---

# Summary

:::tip Main Points

- To be able to reference an object class we need to retrieve a handle for the class. We also need handles for the attributes
- To be able to register and discover objects of a particular class as well as update/reflect attributes we need to publish and subscribe to it
- The UpdateAttributeValues is used to send an update for a set of attributes for a specific object instance
- Updates are typically sent when the value has changed or when another federate needs and update.
- Your federate receives the ReflectAttributeValues with updated attribute values for attributes that is subscribes to