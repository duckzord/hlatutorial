---
sidebar_position: 8
---

# Lab 5: Developing a FOM for Object Classes

In this lab we will study the FOM and the object classes in particular.
## A look at object classes
Do the following:
1. To open the FOM start Pitch Visual OMT Free and select the Fuel Economy FOM project in the start dialog.
2. Inspect the tree of object classes. There are actually only two classes: the Object Root and the Car. Open and close the attribute list of the Car class using the small triangle. You may want to increase the width of the column to read the full names. Double-click on the Car class to inspect it.
3. Go to the data types and look at the Enumerated data types. Here you should inspect the FuelTypeEnum32.
4. Go to the data types and look at the Fixed Record data types. Here you should inspect the PositionRec. Note how it builds upon the AngleFloat32 data type. Can you find the definition of that data type?
5. Now try and modify some parts of the FOM. Add your own class FuelStation with attributes Name, Position, HasDiesel and HasPetrol. Add more data types.
6. Note that you cannot save your modified FOM using the Free version of Pitch Visual OMT.
7. Shut down Pitch Visual OMT