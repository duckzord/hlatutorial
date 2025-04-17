---
sidebar_position: 1
---

# Introduction

You may already have noted some shortcomings of the Fuel Economy Federation that relates to time. There is no coordination of the simulated time in the federation, with the exception that the simulation time is started and stopped in all federates using start and stop interactions. One computer may have a clock that runs a little faster than the other ones. There are also smaller or larger delays in communication between the computers. This means that a federate that compares the position of a local and a remote car may compare the position of a local car at time 10 with the position of a remote car at time 9. The result of such a simulation is incorrect. In some cases, some minor errors may be acceptable, in other cases not. Fortunately, HLA provides services that guarantee correct time management, no matter how fast our federation runs. In this chapter we will have a look at them. 

We will now add HLA time management to the Fuel Economy Federation. The Federation Agreement in Appendix A specifies the following for the Fuel Economy Federation: “The federation shall be time managed using HLA Time Management. The Master federate shall determine the speed of the execution, which could be real-time, scaled real-time or as fast-as-possible. The standardized time representation HLAinteger64Time shall be used. This integer shall represent the number of microseconds elapsed since the start of the execution. All executions shall start at logical time zero with all time managed federates joined.” 

This chapter shows how to implement this. Finally, it provides the most important principles and definitions of HLA Time management. Before we start working with the federation, we need to describe a few concepts.

