---
sidebar_position: 1
---

# Introduction to FOM Modules

We will continue with the Fuel Economy Federation from Part 1 of the HLA Tutorial. The first thing that we want to do is to split up the FOM into FOM modules. These modules contain the same type of things as a FOM, for example object classes with attributes, interactions with parameters and data types. There are several reasons for splitting a FOM into modules but they all relate to separation of concern:

- Different teams may develop and maintain different parts of a FOM
- It is easier to reuse certain parts of a FOM between different projects
- New combinations of FOM modules can be used for new projects

We have already used FOM modules in Part 1 of the tutorial without mentioning it explicitly. To be more exact: our FOM has used a number of concepts that are defined in another module. HLA has a predefined, standardized FOM module that is called the Management and Initialization Module, or in short: the MIM. We will describe the MIM in further detail later in the next chapter. 

